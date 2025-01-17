<template>
  <div>
    <h2 class="page-title-bar">
      <i class="ico ico-user"></i>{{ $t('User Info') }}
    </h2>
    <div class="searchArea">
      <v-text-field
        v-model="searchCondition.email"
        @keyup.enter="clickSearch"
        outlined
        dense
        hide-details
        :label="$t('Email')"
        :placeholder="$t('Input the Email')"
        class="form-input"
        clearable
      ></v-text-field>
      <v-text-field
        v-model="searchCondition.firstName"
        @keyup.enter="clickSearch()"
        :label="$t('Name')"
        :placeholder="`${$t('Input the user name')}`"
        class="form-input ml-3"
        clearable
        outlined
        dense
        hide-details
      ></v-text-field>
      <v-select
        v-model="searchCondition.accessLevel"
        :label="$t('User Level')"
        :placeholder="$t('Select the user level')"
        :items="accessLevelItems"
        class="form-select ml-3"
        item-text="name"
        item-value="level"
        outlined
        dense
        hide-details
        clearable
      ></v-select>
      <v-btn @click="clickSearch" text class="btn type-search ml-3"
        >{{ $t('Search') }}
      </v-btn>
    </div>
    <v-data-table
      v-model="selected"
      @click:row="openUserEditModal"
      :headers="tableHeaders"
      :items="tableItems"
      :item-class="getRowClass"
      :hide-default-footer="true"
      :options.sync="options"
      item-key="email"
      :items-per-page="10"
      :show-select="false"
      class="tbl-type01 mt-10"
    >
      <template slot="no-data">
        <p>{{ $t('No data available') }}</p>
      </template>
    </v-data-table>
    <userEditPopup
      :dialogUserEdit="dialogUserEdit && !btnDisabledDetail"
      :item="userEditItem"
      :accessLevelItems="accessLevelItems"
      :userAccessLevel="userAccessLevel"
      @closeModal="closeUserEditModal"
      @updateUserInfo="paging"
    ></userEditPopup>
    <div class="table-options">
      <div>
        <userNewPopup
          :accessLevelItems="accessLevelItems"
          :userAccessLevel="userAccessLevel"
          :btnDisabledNewDelete="btnDisabledNewDelete"
          @updateUserInfo="paging"
        ></userNewPopup>
        <v-btn
          :disabled="btnDisabledNewDelete || checkSelected"
          @click="clickDelete"
          class="btn ml-2"
          text
          >{{ $t('Delete') }}
        </v-btn>
        <v-btn
          :disabled="btnDisabledExport || btnDisabledExportCheckList"
          @click="exportUserInfoList"
          class="btn ml-2"
          text
        >
          {{ $t('Export') }}
        </v-btn>
      </div>
      <div>
        <div class="pageInfo">{{ pageInfoText }}</div>
        <div class="pagination2">
          <v-text-field
            v-model="goToPageInput"
            class="form-input noneline"
            placeholder="Page"
            outlined
            dense
            hide-details
            solo
            @keyup.enter="goToPage(goToPageInput, paging, pageCount)"
          ></v-text-field>

          <button
            @click="goToPage(goToPageInput, paging, pageCount)"
            type="button"
            class="btnGoToPage"
          >
            <i
              class="v-icon notranslate mdi mdi-chevron-right theme--light"
              aria-hidden="true"
            >
            </i>
          </button>
          <!-- 페이지 앞 뒤 이동 -->
          <button
            @click="goTenPageBackwards(page, paging)"
            :class="page < 10 ? 'pagination-nav-disabled' : null"
            class="pagination-nav pagination-nav-prev"
            type="button"
          >
            <img
              src="@/assets//img/ico-paging-prev.png"
              alt="이전 10페이지 이동"
            />
          </button>
          <v-pagination
            v-model="page"
            @input="paging"
            :length="pageCount * 1 || 1"
            :total-visible="10"
            color="#2f3b4c"
            style="display: block;"
          ></v-pagination>
          <button
            @click="goTenPageForward(page, paging, pageCount)"
            :class="page + 10 > pageCount ? 'pagination-nav-disabled' : null"
            class="pagination-nav pagination-nav-next"
            type="button"
          >
            <img
              src="@/assets//img/ico-paging-next.png"
              alt="다음 10페이지 이동"
            />
          </button>
        </div>
      </div>
    </div>
    <a ref="link" :style="{ display: 'none' }" />
  </div>
</template>

<script>
import EventBus from '@/plugins/eventBus'
import commons from '@/plugins/commons'
import codes from '@/plugins/codes'
import { exportFiles } from '@/plugins/exporter'
import { setTempObj, getTempObj } from '@/plugins/sessionStorageManager'

import userEditPopup from './modal/UserInfoEditPopupCloud'
import userNewPopup from './modal/UserInfoNewPopup'
// Mixins
import Pagenation from '@/mixins/Pagenation'

export default {
  name: 'UserInfo',
  mixins: [Pagenation],
  components: {
    userEditPopup,
    userNewPopup
  },
  data () {
    return {
      myAccessLevel: Number(
        this.$store.state.auth.user.accountInfo.accessLevel
      ),
      productionType: process.env.VUE_APP_PRODUCTION_TYPE,
      cloudMode:
        process.env.VUE_APP_PRODUCTION_TYPE === codes.productionTypes.CLOUD,
      userAccessLevel: null,
      btnDisabledNewDelete: null,
      btnDisabledDetail: null,
      btnDisabledExport: null,
      accessLevelItems: [],
      page: 0,
      pageCount: 0,
      pageInfoText: null,
      goToPageInput: null,
      tableItems: [],
      selected: [],
      options: {},
      ROW_CLASS: 'row-class',
      searchParam: {
        company: '',
        email: '',
        firstName: '',
        accessLevel: '',
        size: '10',
        page: '',
        sort: ''
      },
      searchCondition: {
        email: '',
        firstName: '',
        accessLevel: ''
      },
      dialogUserEdit: false,
      userEditItem: {},

      requestConfig: {}
    }
  },
  computed: {
    tableHeaders () {
      return [
        {
          text: this.$t('Email'),
          sortable: true,
          value: 'emailAddress',
          width: '20%'
        },
        {
          text: this.$t('NAME'),
          sortable: true,
          value: 'firstName',
          width: '20%'
        },
        {
          text: this.$t('User Level'),
          sortable: true,
          value: 'accessLevel',
          width: '15%'
        },
        {
          text: this.$t('Approved'),
          sortable: true,
          value: 'isApproved',
          width: '15%'
        },
        {
          text: this.$t('STORE MAPPING'),
          sortable: false,
          value: 'managedStoreCount',
          width: '15%'
        },
        {
          text: this.$t('LAST MODIFIED DATE'),
          sortable: true,
          value: 'lastModifiedDate'
        }
      ]
    },
    btnDisabledExportCheckList () {
      var flag = true
      if (this.tableItems.length) flag = false
      return flag
    },
    checkSelected () {
      var flag = true
      if (this.selected.length) flag = false
      return flag
    }
  },
  watch: {
    options: function (val) {
      let sortParam = ''
      if (val.sortBy.length && val.sortDesc[0]) {
        sortParam += val.sortBy[0] + ',DESC'
      } else if (val.sortBy.length && !val.sortDesc[0]) {
        sortParam += val.sortBy[0] + ',ASC'
      }
      this.searchParam.sort = sortParam
      this.page = 1
      this.searchAccountList()
    },
    searchCondition: {
      handler (newSearchCondition) {
        const userInfo = {
          searchCondition: newSearchCondition,
          searchParam: this.searchParam
        }
        setTempObj('userInfo', userInfo)
      },
      deep: true
    }
  },
  mounted () {
    // button 권한 체크
    // User Info : New / Delete
    this.$store.dispatch('auth/getDisabledBtn', '8100').then(flag => {
      if (this.cloudMode) {
        this.btnDisabledNewDelete = true
      } else {
        this.btnDisabledNewDelete = flag
      }
    })
    // // User Info : Detail Popup
    this.$store.dispatch('auth/getDisabledBtn', '8101').then(flag => {
      this.btnDisabledDetail = flag
    })
    // //  User Info : Export
    this.$store.dispatch('auth/getDisabledBtn', '8102').then(flag => {
      this.btnDisabledExport = flag
    })
    EventBus.$emit('enableSelectedStores', false)
    this.searchParam.company = this.$store.state.auth.user.company
    // 검색조건 설정
    const userInfoSessionData = getTempObj('userInfo')
    if (!commons.isNull(userInfoSessionData)) {
      if (!commons.isNull(userInfoSessionData.searchCondition)) {
        this.searchCondition = userInfoSessionData.searchCondition
      }
      Object.keys(this.searchCondition).forEach(key => {
        this.searchParam[key] = this.searchCondition[key]
      })
    }
    this.getUserAccessLevel()
    this.getUserLevel()
    this.searchAccountList()
  },
  methods: {
    getPageInfoText (headers, tabelItems) {
      return (
        headers['x-number'] * 1 * headers['x-size'] +
        1 +
        ' to ' +
        (headers['x-number'] * 1 * headers['x-size'] + tabelItems.length) +
        ', ' +
        headers['x-totalelements'] * 1 +
        ' in total'
      )
    },
    convertDate (date) {
      if (commons.isNull(date)) return '-'
      date = new Date(date)

      const utcDate = {
        year: date.getFullYear(),
        month: date.getMonth() + 1,
        day: date.getDate(),
        hours: date.getHours(),
        minutes: date.getMinutes(),
        seconds: date.getSeconds()
      }
      for (const key of Object.keys(utcDate)) {
        if (utcDate[key] < 10) utcDate[key] = `0${utcDate[key]}`
      }
      return `${utcDate.year}-${utcDate.month}-${utcDate.day} ${utcDate.hours}:${utcDate.minutes}:${utcDate.seconds}`
    },
    convertResponseAccountList (accountList) {
      return accountList.map(responseAccount => {
        const convertedAccount = {}
        convertedAccount.account = responseAccount.account
        convertedAccount.emailAddress = responseAccount.emailAddress
        convertedAccount.firstName = responseAccount.firstName
        convertedAccount.accessLevel = responseAccount.accessLevel
        convertedAccount.isApproved = responseAccount.isApproved
        convertedAccount.managedStoreCount = responseAccount.managedStoreCount
        convertedAccount.lastModifiedDate = this.convertDate(
          responseAccount.lastModifiedDate
        )
        convertedAccount.customer = responseAccount.customer
        return convertedAccount
      })
    },
    searchAccountList () {
      const config = { params: this.searchParam }
      config.params.page = this.page - 1
      this.$utils
        .callAxios(
          codes.requests.getUsersCloud.method,
          codes.requests.getUsersCloud.url,
          config
        )
        .then(res => {
          this.saveRequestConfig(res.config)
          const headers = res.headers
          if (res.data) {
            this.tableItems = this.convertResponseAccountList(
              res.data.accountList
            )
          } else this.tableItems = []
          this.pageInfoText = this.getPageInfoText(headers, this.tableItems)
          this.page = headers['x-number'] * 1 + 1
          this.pageCount = headers['x-totalpages'] * 1
          this.selected = []
        })
    },
    getUserAccessLevel () {
      const config = { params: {} }
      config.params = commons.copy(this.searchParam)
      config.params.account = this.$store.state.auth.user.account
      if (this.productionType === 'cloud') {
        config.params.company = this.$store.state.auth.user.company
      }
      this.$utils
        .callAxios(
          codes.requests.getUsers.method,
          codes.requests.getUsers.url,
          config
        )
        .then(res => {
          if (res.data) {
            this.userAccessLevel = res.data.accountList.map(
              data => data.accessLevel
            )[0]
          }
        })
    },
    getUserLevel () {
      const config = {
        params: {
          company: this.$store.state.auth.user.company
        }
      }
      this.$utils
        .callAxios(
          codes.requests.getUserAccessLevel.method,
          codes.requests.getUserAccessLevel.url,
          config
        )
        .then(res => {
          if (res.data) {
            this.accessLevelItems = res.data.accessLevelList.map(data => {
              const obj = {}
              obj.name = `${data.title} (${data.accessLevel})`
              obj.level = data.accessLevel
              return obj
            })
          }
        })
    },
    paging (page = this.page) {
      this.page = Number(page)
      this.goToPageInput = page
      this.searchAccountList(page)
    },
    clickSearch () {
      Object.keys(this.searchCondition).forEach(key => {
        this.searchParam[key] = this.searchCondition[key]
      })
      this.page = 1
      this.searchAccountList()
    },
    openUserEditModal (item) {
      if (Number(item.accessLevel) < this.myAccessLevel) return
      this.closeUserEditModal(false)
      this.userEditItem = item
      EventBus.$emit('openUserInfoEditPopup', this.userEditItem)
      this.dialogUserEdit = true
    },
    closeUserEditModal (state) {
      this.dialogUserEdit = state
    },
    saveRequestConfig (config) {
      const requestConfig = {
        url: config.url,
        method: config.method,
        params: config.params
      }
      this.requestConfig = requestConfig
    },
    exportUserInfoList () {
      exportFiles(this.requestConfig, this.$refs.link, 'UserInfoList.xlsx')
    },
    getRowClass () {
      return codes.ROW_CLASS
    },
    clickDelete () {
      this.selected.forEach(item => {
        const config = {
          params: {
            company: this.$store.state.auth.user.company,
            myAccessLevel: this.userAccessLevel,
            account: item.account
          }
        }
        this.$utils
          .callAxios(
            codes.requests.deleteUser.method,
            codes.requests.deleteUser.url,
            config
          )
          .then(res => {
            this.selected = []
            this.paging()
          })
          .catch(error => {
            if (error.response.status === 405) {
              EventBus.$emit(
                'messageAlert',
                this.$t('Users above their own level cannot be deleted.')
              )
            }
            this.selected = []
            this.paging()
          })
      })
    }
  }
}
</script>
<style>
.row-class:hover {
  cursor: pointer;
}
</style>
