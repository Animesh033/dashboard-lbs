<template>
  <div>
    <h2 class="page-title-bar">
      <i class="ico ico-system"></i>{{ $t('Dashboard Config') }}
    </h2>

    <h3 class="tit-group mt-10">{{ $t('Alert Setting') }}</h3>

    <div class="settingBox">
      <v-row>
        <v-col>
          <h4 class="tit-section-sub">{{ $t('Label Status') }}</h4>
          <div>
            <p class="label-txt">{{ $t('Update Failure') }}</p>
            <div class="innerBox">
              <v-text-field
                outlined
                dense
                hide-details
                solo
                suffix="%"
                :prepend-icon="`${$t('Caution')}`"
                append-outer-icon="~"
                v-model="labelUpdatedCaution"
                class="form-input appendIcon"
                type="number"
                @keyup.prevent="handleKeyUp"
                clearable
              ></v-text-field>
              <v-text-field
                outlined
                dense
                hide-details
                solo
                suffix="%"
                :prepend-icon="`${$t('Danger')}`"
                append-outer-icon="~"
                v-model="labelUpdatedDanger"
                class="form-input appendIcon"
                type="number"
                @keyup.prevent="handleKeyUp"
                clearable
              ></v-text-field>
            </div>
          </div>
        </v-col>
        <v-col>
          <h4 class="tit-section-sub">{{ $t('Gateway Status') }}</h4>
          <div>
            <p class="label-txt">{{ $t('Offline') }}</p>
            <div class="innerBox">
              <v-text-field
                outlined
                dense
                hide-details
                solo
                suffix="%"
                :prepend-icon="`${$t('Caution')}`"
                append-outer-icon="~"
                v-model="gwOfflineCaution"
                class="form-input appendIcon"
                type="number"
                @keyup.prevent="handleKeyUp"
                clearable
              ></v-text-field>
              <v-text-field
                outlined
                dense
                hide-details
                solo
                suffix="%"
                :prepend-icon="`${$t('Danger')}`"
                append-outer-icon="~"
                v-model="gwOfflineDanger"
                class="form-input appendIcon"
                type="number"
                @keyup.prevent="handleKeyUp"
                clearable
              ></v-text-field>
            </div>
          </div>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <h4 class="tit-section-sub">{{ $t('Exception Status') }}</h4>
          <v-row>
            <v-col>
              <div>
                <p class="label-txt">{{ $t('Label Offline') }}</p>
                <div class="innerBox">
                  <v-text-field
                    outlined
                    dense
                    hide-details
                    solo
                    suffix="%"
                    :prepend-icon="`${$t('Caution')}`"
                    append-outer-icon="~"
                    v-model="labelOfflineCaution"
                    class="form-input appendIcon"
                    type="number"
                    @keyup.prevent="handleKeyUp"
                    clearable
                  ></v-text-field>
                  <v-text-field
                    outlined
                    dense
                    hide-details
                    solo
                    suffix="%"
                    :prepend-icon="`${$t('Danger')}`"
                    append-outer-icon="~"
                    v-model="labelOfflineDanger"
                    class="form-input appendIcon"
                    type="number"
                    @keyup.prevent="handleKeyUp"
                    clearable
                  ></v-text-field>
                </div>
              </div>
            </v-col>
            <v-col>
              <div>
                <p class="label-txt">{{ $t('Low Battery') }}</p>
                <div class="innerBox">
                  <v-text-field
                    outlined
                    dense
                    hide-details
                    solo
                    suffix="%"
                    :prepend-icon="`${$t('Caution')}`"
                    append-outer-icon="~"
                    v-model="labelLowBatteryCaution"
                    class="form-input appendIcon"
                    type="number"
                    @keyup.prevent="handleKeyUp"
                    clearable
                  ></v-text-field>
                  <v-text-field
                    outlined
                    dense
                    hide-details
                    solo
                    suffix="%"
                    :prepend-icon="`${$t('Danger')}`"
                    append-outer-icon="~"
                    v-model="labelLowBatteryDanger"
                    class="form-input appendIcon"
                    type="number"
                    @keyup.prevent="handleKeyUp"
                    clearable
                  ></v-text-field>
                </div>
              </div>
            </v-col>
          </v-row>
          <v-row class="pt-10">
            <v-col>
              <div>
                <p class="label-txt">{{ $t('Bad Signal') }}</p>
                <div class="innerBox">
                  <v-text-field
                    outlined
                    dense
                    hide-details
                    solo
                    suffix="%"
                    :prepend-icon="`${$t('Caution')}`"
                    append-outer-icon="~"
                    v-model="labelSignalCaution"
                    class="form-input appendIcon"
                    type="number"
                    @keyup.prevent="handleKeyUp"
                    clearable
                  ></v-text-field>
                  <v-text-field
                    outlined
                    dense
                    hide-details
                    solo
                    suffix="%"
                    :prepend-icon="`${$t('Danger')}`"
                    append-outer-icon="~"
                    v-model="labelSignalDanger"
                    class="form-input appendIcon"
                    type="number"
                    @keyup.prevent="handleKeyUp"
                    clearable
                  ></v-text-field>
                </div>
              </div>
            </v-col>
            <v-col>
              <div>
                <p class="label-txt">{{ $t('Misused') }}</p>
                <div class="innerBox">
                  <v-text-field
                    outlined
                    dense
                    hide-details
                    solo
                    suffix="%"
                    :prepend-icon="`${$t('Caution')}`"
                    append-outer-icon="~"
                    v-model="labelMisusedCaution"
                    class="form-input appendIcon"
                    type="number"
                    @keyup.prevent="handleKeyUp"
                    clearable
                  ></v-text-field>
                  <v-text-field
                    outlined
                    dense
                    hide-details
                    solo
                    suffix="%"
                    :prepend-icon="`${$t('Danger')}`"
                    append-outer-icon="~"
                    v-model="labelMisusedDanger"
                    class="form-input appendIcon"
                    type="number"
                    @keyup.prevent="handleKeyUp"
                    clearable
                  ></v-text-field>
                </div>
              </div>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </div>
    <div>
      <v-btn
        text
        :disabled="btnDisabledAlertSetting"
        @click="clickSave"
        class="btn t-bottom"
        >{{ $t('Save') }}</v-btn
      >
      <v-btn
        text
        :disabled="btnDisabledAlertSetting"
        @click="clickReset"
        class="btn t-bottom ml-2"
        >{{ $t('Reset') }}</v-btn
      >
    </div>

    <!-- 10.22 추가 -->
    <h3 class="tit-group mt-10">{{ $t('Alive Interval') }}</h3>
    <v-text-field
      outlined
      dense
      hide-details
      solo
      v-model="aliveInterval"
      min="0"
      class="form-input"
      style="width:200px"
      type="number"
      @keyup.prevent="handleKeyUp"
    ></v-text-field>
    <v-btn text class="btn-s mt-2" @click="clickIntervalSave">{{
      $t('Save')
    }}</v-btn>
    <!-- //10.22 추가 -->

    <div :class="{ hidden: this.SingleUser }">
      <h3 class="tit-group mt-10">{{ $t('Area Group Management') }}</h3>
      <v-row>
        <v-col cols="3">
          <div class="areaGroup">
            <h4 class="tit">{{ $t('Company') }}</h4>
            <v-list-item-group v-model="selectedCompany" @change="clickCompany">
              <v-virtual-scroll
                :items="companyList"
                :item-height="50"
                height="250"
                class="scroll-selector"
              >
                <template v-slot="{ item }">
                  <v-list-item :key="item" :value="item">
                    <v-list-item-title v-text="item"></v-list-item-title>
                  </v-list-item>
                </template>
              </v-virtual-scroll>
            </v-list-item-group>
          </div>
          <!-- 10.05 수정 -->
          <div class="area-btn-group">
            <v-btn
              text
              @click="clickAreaBtn('new', 'company')"
              :disabled="btnController.isSolumAdmin"
              class="btn"
              >{{ $t('New') }}</v-btn
            >
            <v-btn
              text
              :disabled="btnController.isSolumAdmin"
              @click="clickAreaBtn('edit', 'company')"
              class="btn ml-1"
              >{{ $t('Edit') }}</v-btn
            >
            <v-btn
              text
              :disabled="true"
              @click="deleteArea('company')"
              class="btn ml-1"
              >{{ $t('Delete') }}</v-btn
            >
          </div>
        </v-col>
        <v-col cols="3">
          <div class="areaGroup">
            <h4 class="tit">{{ $t('Country') }}</h4>
            <v-list-item-group v-model="selectedCountry" @change="clickCountry">
              <v-virtual-scroll
                :items="countryList"
                :item-height="50"
                height="250"
                class="scroll-selector"
              >
                <template v-slot="{ item }">
                  <v-list-item :key="item" :value="item">
                    <v-list-item-title v-text="item"></v-list-item-title>
                  </v-list-item>
                </template>
              </v-virtual-scroll>
            </v-list-item-group>
          </div>
          <!-- 10.05 수정 -->
          <div class="area-btn-group">
            <v-btn
              text
              @click="clickAreaBtn('new', 'country')"
              :disabled="btnController.company"
              class="btn"
              >{{ $t('New') }}</v-btn
            >
            <v-btn
              text
              @click="clickAreaBtn('edit', 'country')"
              :disabled="btnController.country"
              class="btn ml-1"
              >{{ $t('Edit') }}</v-btn
            >
            <v-btn
              text
              :disabled="btnController.country"
              @click="deleteArea('country')"
              class="btn ml-1"
              >{{ $t('Delete') }}</v-btn
            >
          </div>
          <!-- //10.05 수정 -->
        </v-col>
        <v-col cols="3">
          <div class="areaGroup">
            <h4 class="tit">{{ $t('Region') }}</h4>

            <v-list-item-group v-model="selectedRegion" @change="clickRegion">
              <v-virtual-scroll
                :items="regionList"
                :item-height="50"
                height="250"
                class="scroll-selector"
              >
                <template v-slot="{ item }">
                  <v-list-item :key="item" :value="item">
                    <v-list-item-title v-text="item"></v-list-item-title>
                  </v-list-item>
                </template>
              </v-virtual-scroll>
            </v-list-item-group>
          </div>
          <!-- 10.05 수정 -->
          <div class="area-btn-group">
            <v-btn
              text
              @click="clickAreaBtn('new', 'region')"
              :disabled="btnController.country"
              class="btn"
              >{{ $t('New') }}</v-btn
            >
            <v-btn
              text
              @click="clickAreaBtn('edit', 'region')"
              :disabled="btnController.region"
              class="btn ml-1"
              >{{ $t('Edit') }}</v-btn
            >
            <v-btn
              text
              :disabled="btnController.region"
              @click="deleteArea('region')"
              class="btn ml-1"
              >{{ $t('Delete') }}</v-btn
            >
          </div>
          <!-- //10.05 수정 -->
        </v-col>
        <v-col cols="3">
          <div class="areaGroup">
            <h4 class="tit">{{ $t('City') }}</h4>
            <v-list-item-group v-model="selectedCity">
              <v-virtual-scroll
                :v-model="cityList"
                :items="cityList"
                :item-height="50"
                height="250"
                class="scroll-selector"
              >
                <template v-slot="{ item }">
                  <v-list-item :key="item" :value="item">
                    <v-list-item-title v-text="item"></v-list-item-title>
                  </v-list-item>
                </template>
              </v-virtual-scroll>
            </v-list-item-group>
          </div>
          <!-- 10.05 수정 -->
          <div class="area-btn-group">
            <v-btn
              text
              @click="clickAreaBtn('new', 'city')"
              :disabled="btnController.region"
              class="btn"
              >{{ $t('New') }}</v-btn
            >
            <v-btn
              text
              @click="clickAreaBtn('edit', 'city')"
              :disabled="btnController.city"
              class="btn ml-1"
              >{{ $t('Edit') }}</v-btn
            >
            <v-btn
              text
              :disabled="btnController.city"
              @click="deleteArea('city')"
              class="btn ml-1"
              >{{ $t('Delete') }}</v-btn
            >
          </div>
          <!-- //10.05 수정 -->
        </v-col>
        <areaSettingModal
          :dialog="dialogArea"
          :action="actionAreaModal"
          :category="categoryAreaModal"
          :item="valueAreaModal"
          @saveArea="saveArea"
          @closeAreaModal="closeAreaSettingModal"
        />
        <companySettingModal
          :dialogCompany="dialogCompany"
          :action="actionAreaModal"
          :category="categoryAreaModal"
          :item="valueAreaModal"
          @saveCompany="saveCompany"
          @closeCompanyModal="closeCompanySettingModal"
        />
      </v-row>
    </div>
    <!--2020.10.27 Defalt Password Setting 부분은 가려 주세요. 구현 보류된 부분입니다. - 여동협 -->
    <div style="display: none;">
      <!-- 10.22 추가 -->
      <h3 class="tit-group mt-10">Defalt Password Setting</h3>

      <div class="settingBox">
        <v-row>
          <v-col cols="4">
            <v-text-field
              outlined
              dense
              hide-details
              label="Password"
              type="password"
              class="form-input"
            ></v-text-field>
          </v-col>
          <v-col cols="4">
            <v-text-field
              outlined
              dense
              hide-details
              label="Confirm Password"
              type="password"
              class="form-input"
            ></v-text-field>
          </v-col>
        </v-row>
      </div>
      <div>
        <v-btn text class="btn t-bottom">{{ $t('Save') }}</v-btn>
      </div>
    </div>
    <!-- //10.22 추가 -->
  </div>
</template>

<script>
import areaSettingModal from './modal/DashboardAreaSettingModal'
import companySettingModal from './modal/DashboardCompanySettingModal'
import EventBus from '@/plugins/eventBus.js'
import commons from '@/plugins/commons'

export default {
  name: 'DashboardConfig',
  components: {
    areaSettingModal,
    companySettingModal
  },

  data () {
    return {
      serverType: process.env.VUE_APP_PRODUCTION_TYPE,
      isSolumAdmin: this.$store.state.auth.user.isSolumAdmin,
      SingleUser: false,
      dialog: false,
      dialog1: false,

      // 버튼 권한 관련
      btnDisabledAlertSetting: null,
      btnDisabledAreaSetting: null,

      // Alert Setting 관련
      labelUpdatedCaution: null,
      labelUpdatedDanger: null,
      gwOfflineCaution: null,
      gwOfflineDanger: null,
      labelOfflineCaution: null,
      labelOfflineDanger: null,
      labelLowBatteryCaution: null,
      labelLowBatteryDanger: null,
      labelSignalCaution: null,
      labelSignalDanger: null,
      labelMisusedCaution: null,
      labelMisusedDanger: null,

      // Alive Interval
      aliveInterval: null,

      companyData: {},
      areaData: {},

      countryList: [],
      regionList: [],
      cityList: [],

      selectedCompany: null,
      selectedCountry: null,
      selectedRegion: null,
      selectedCity: null,

      inputCompany: null,
      inputCountry: null,
      inputRegion: null,
      inputCity: null,

      rules: {
        labelUpdatedDangerRule: [
          v => Number(v) >= Number(this.labelUpdatedCaution) || 'Error'
        ],
        gwOfflineDangerRule: [
          v => Number(v) >= Number(this.gwOfflineCaution) || 'Error'
        ],
        labelOfflineDangerRule: [
          v => Number(v) >= Number(this.labelOfflineCaution) || 'Error'
        ],
        labelLowBatteryDangerRule: [
          v => Number(v) >= Number(this.labelLowBatteryCaution) || 'Error'
        ],
        labelSignalDangerRule: [
          v => Number(v) >= Number(this.labelSignalCaution) || 'Error'
        ],
        labelMisusedDangerRule: [
          v => Number(v) >= Number(this.labelMisusedCaution) || 'Error'
        ]
      },

      dialogArea: false,
      dialogCompany: false,
      actionAreaModal: null,
      categoryAreaModal: null,
      valueAreaModal: null
    }
  },
  computed: {
    companyList () {
      return Object.keys(this.companyData).filter(element => element !== '')
    },
    btnController () {
      const controller = {
        isSolumAdmin: !this.isSolumAdmin,
        company: true,
        country: true,
        region: true,
        city: true
      }
      if (this.selectedCompany) {
        controller.company = false || this.btnDisabledAreaSetting
      }
      if (this.selectedCountry) {
        controller.country = false || this.btnDisabledAreaSetting
      }
      if (this.selectedRegion) {
        controller.region = false || this.btnDisabledAreaSetting
      }
      if (this.selectedCity) {
        controller.city = false || this.btnDisabledAreaSetting
      }

      return controller
    },
    alertSettingValidation () {
      return (
        Number(this.labelUpdatedDanger) >= Number(this.labelUpdatedCaution) &&
        Number(this.gwOfflineDanger) >= Number(this.gwOfflineCaution) &&
        Number(this.labelOfflineDanger) >= Number(this.labelOfflineCaution) &&
        Number(this.labelLowBatteryDanger) >=
          Number(this.labelLowBatteryCaution) &&
        Number(this.labelSignalDanger) >= Number(this.labelSignalCaution) &&
        Number(this.labelMisusedDanger) >= Number(this.labelMisusedCaution)
      )
    }
  },
  watch: {},
  methods: {
    handleKeyUp (e) {
      const koreanExp = /[ㄱ-ㅎㅏ-ㅣ가-힣]/g
      e.target.value = e.target.value.replace(koreanExp, '')
    },
    getAlertSetting () {
      const url = '/api/common/config/alertsetting'
      const config = {}
      if (this.serverType === 'cloud') {
        config.params = { company: this.$store.state.auth.user.company }
      }
      this.$utils.callAxios('get', url, config).then(res => {
        if (res.data) {
          this.gwOfflineCaution = res.data.gwOfflineCaution
          this.gwOfflineDanger = res.data.gwOfflineDanger
          this.labelUpdatedCaution = res.data.labelUpdatedCaution
          this.labelUpdatedDanger = res.data.labelUpdatedDanger
          this.labelLowBatteryCaution = res.data.labelLowBatteryCaution
          this.labelLowBatteryDanger = res.data.labelLowBatteryDanger
          this.labelOfflineCaution = res.data.labelOfflineCaution
          this.labelOfflineDanger = res.data.labelOfflineDanger
          this.labelSignalCaution = res.data.labelSignalCaution
          this.labelSignalDanger = res.data.labelSignalDanger
          this.labelMisusedCaution = res.data.labelMisusedCaution
          this.labelMisusedDanger = res.data.labelMisusedDanger
        }
      })
    },
    clickIntervalSave () {
      if (this.aliveInterval) {
        const url = '/api/common/config/aliveInterval'
        const config = {
          params: {
            company: this.$store.state.auth.user.company,
            aliveInterval: this.aliveInterval
          }
        }
        const body = {}
        this.$utils.callAxiosWithBody('put', url, body, config).then(res => {
          this.$store.dispatch('auth/UPDATE_INTERVAL', this.aliveInterval)
          EventBus.$emit('messageAlert', this.$t(res.data.responseMessage))
        })
      } else {
        EventBus.$emit('messageAlert', this.$t('input error'))
      }
    },
    clickSave () {
      if (this.alertSettingValidation) {
        const url = '/api/common/config/alertsetting'
        const config = {
          params: { company: this.$store.state.auth.user.company }
        }
        const body = {
          gwOfflineCaution: this.gwOfflineCaution,
          gwOfflineDanger: this.gwOfflineDanger,
          labelUpdatedCaution: this.labelUpdatedCaution,
          labelUpdatedDanger: this.labelUpdatedDanger,
          labelLowBatteryCaution: this.labelLowBatteryCaution,
          labelLowBatteryDanger: this.labelLowBatteryDanger,
          labelOfflineCaution: this.labelOfflineCaution,
          labelOfflineDanger: this.labelOfflineDanger,
          labelSignalCaution: this.labelSignalCaution,
          labelSignalDanger: this.labelSignalDanger,
          labelMisusedCaution: this.labelMisusedCaution,
          labelMisusedDanger: this.labelMisusedDanger
        }
        this.$utils.callAxiosWithBody('post', url, body, config).then(res => {
          EventBus.$emit('messageAlert', this.$t(res.data.responseMessage))
          this.getAlertSetting()
        })
      } else {
        EventBus.$emit('messageAlert', this.$t('input error'))
      }
    },
    clickReset () {
      const url = '/api/common/config/alertsetting'
      const config = {
        params: { company: this.$store.state.auth.user.company }
      }
      const body = null
      this.$utils.callAxiosWithBody('post', url, body, config).then(res => {
        EventBus.$emit('messageAlert', this.$t(res.data.responseMessage))
        this.getAlertSetting()
      })
    },
    getCompany () {
      if (!this.isSolumAdmin) {
        this.companyData = {}
        this.companyData[this.$store.state.auth.user.company] = {}
        return
      }

      const url = '/api/common/company' // area ,  company
      const config = {
        params: {
          //   company: this.$store.state.auth.user.company
        }
      }
      this.$utils.callAxios('get', url, config).then(res => {
        this.companyData = {}
        if (res.data) {
          res.data.companyList.map(data => {
            this.companyData[data.code] = {}
          })
        } else this.companyData = {}
      })
    },
    async getArea () {
      const url = '/api/common/area'
      const config = {
        params: {
          company: this.selectedCompany
        }
      }
      return this.$utils.callAxios('get', url, config).then(async res => {
        if (res.data) {
          this.areaData = await this.loadAreaData(res.data.areaParamList)
          this.getCountryList()
          this.getRegionList()
          this.getCityList()
          return this.areaData
        } else {
          return {}
        }
      })
    },
    clickCompany () {
      if (commons.isNull(this.selectedCompany)) {
        this.countryList = []
        this.regionList = []
        this.cityList = []
      } else {
        this.selectCompanyList()
      }
    },
    clickCountry () {
      if (commons.isNull(this.selectedCountry)) {
        this.regionList = []
        this.cityList = []
      } else {
        this.getRegionList()
      }
    },
    clickRegion () {
      if (commons.isNull(this.selectedRegion)) {
        this.cityList = []
      } else {
        this.getCityList()
      }
    },
    addCountry () {
      if (this.inputCountry) {
        const url = '/api/common/area'
        const config = {}
        const body = {
          company: '',
          country: this.inputCountry,
          region: '',
          city: ''
        }

        this.$utils.callAxiosWithBody('post', url, body, config).then(res => {
          EventBus.$emit('messageAlert', this.$t(res.data.responseMessage))
          this.getArea()
        })
      } else {
        EventBus.$emit('messageAlert', this.$t('this is empty'))
      }
    },
    addRegion () {
      if (this.inputRegion) {
        const url = '/api/common/area'
        const config = {}
        const body = {
          company: '',
          country: '',
          region: commons.isValue(this.inputRegion),
          city: ''
        }

        this.$utils.callAxiosWithBody('post', url, body, config).then(res => {
          EventBus.$emit('messageAlert', this.$t(res.data.responseMessage))
          this.getArea()
        })
      } else {
        EventBus.$emit('messageAlert', this.$t('this is empty'))
      }
    },
    addCity () {
      if (this.inputCity) {
        const url = '/api/common/area'
        const config = {}
        const body = {
          company: '',
          country: '',
          region: '',
          city: this.inputCity
        }

        this.$utils.callAxiosWithBody('post', url, body, config).then(res => {
          EventBus.$emit('messageAlert', this.$t(res.data.responseMessage))
          this.getArea()
        })
      } else {
        EventBus.$emit('messageAlert', this.$t('this is empty'))
      }
    },
    getCategory (areas, areaName) {
      if (areas[areaName] !== undefined) return areas[areaName]
      else areas[areaName] = {}
      return areas[areaName]
    },
    reloadArea (selectedCompany) {
      alert(selectedCompany)
    },
    async loadAreaData (datas) {
      let areaGroup = this.companyData

      areaGroup = Object.fromEntries(
        Object.entries(this.companyData).map(([key, value]) => [key, {}])
      )

      for await (const data of datas) {
        const company = this.getCategory(areaGroup, data.company)
        const country = this.getCategory(company, data.country)
        const region = this.getCategory(country, data.region)
        this.getCategory(region, data.city)
      }
      return areaGroup
    },
    async selectCompanyList () {
      this.selectedCountry = null
      this.selectedRegion = null
      this.selectedCity = null
      await this.getArea()
      this.getCountryList()
    },
    getCountryList () {
      this.countryList = []
      if (this.selectedCompany) {
        this.countryList = Object.keys(
          this.areaData[this.selectedCompany]
        ).filter(element => element !== '')
      }
    },
    getRegionList () {
      this.regionList = []
      if (this.selectedCompany && this.selectedCountry) {
        this.regionList = Object.keys(
          this.areaData[this.selectedCompany][this.selectedCountry]
        ).filter(element => element !== '')
      }
    },
    getCityList () {
      this.cityList = []
      if (this.selectedCompany && this.selectedCountry && this.selectedRegion) {
        this.cityList = Object.keys(
          this.areaData[this.selectedCompany][this.selectedCountry][
            this.selectedRegion
          ]
        ).filter(element => element !== '')
      }
    },
    clickAreaBtn (action, category) {
      this.actionAreaModal = action
      this.categoryAreaModal = category
      if (category === 'company') this.valueAreaModal = this.selectedCompany
      else if (category === 'country') {
        this.valueAreaModal = this.selectedCountry
      } else if (category === 'region') {
        this.valueAreaModal = this.selectedRegion
      } else if (category === 'city') this.valueAreaModal = this.selectedCity

      if (category === 'company') {
        this.dialogCompany = true
      } else {
        this.dialogArea = true
      }
    },
    closeAreaSettingModal (state) {
      this.dialogArea = state
    },
    closeCompanySettingModal (state) {
      this.dialogCompany = state
    },
    saveArea (action, target, value) {
      if (action === 'new') this.addArea(target, value)
      else if (action === 'edit') this.editArea(target, value)
    },
    saveCompany (action, target, value) {
      // if (action === 'new') this.addArea(target, value)
      // else if (action === 'edit') this.editArea(target, value)

      this.getCompany()
      EventBus.$emit('setManagedStores')
    },
    addArea (target, value) {
      const url = '/api/common/area'
      const config = {
        params: {
          company: this.selectedCompany
        }
      }
      const body = {
        company: '',
        country: '',
        region: '',
        city: ''
      }
      if (target === 'company') {
        body.company = value
      } else if (target === 'country') {
        body.company = this.selectedCompany
        body.country = value
      } else if (target === 'region') {
        body.company = this.selectedCompany
        body.country = this.selectedCountry
        body.region = value
      } else if (target === 'city') {
        body.company = this.selectedCompany
        body.country = this.selectedCountry
        body.region = this.selectedRegion
        body.city = value
      }
      this.$utils.callAxiosWithBody('post', url, body, config).then(res => {
        EventBus.$emit('messageAlert', this.$t(res.data.responseMessage))
        if (target === 'company') this.selectedCompany = null
        else if (target === 'country') this.selectedCountry = null
        else if (target === 'region') this.selectedRegion = null
        else if (target === 'city') this.selectedCity = null
        this.getArea()
        EventBus.$emit('setManagedStores')
      })
    },
    editArea (target, value) {
      const url = '/api/common/area'
      const config = {}
      const body = {
        oldArea: {
          company: '',
          country: '',
          region: '',
          city: ''
        },
        newArea: {
          company: '',
          country: '',
          region: '',
          city: ''
        },
        changedKey: target
      }
      if (target === 'company') {
        body.oldArea.company = this.selectedCompany
        body.newArea.company = value
      } else if (target === 'country') {
        body.oldArea.company = this.selectedCompany
        body.newArea.company = this.selectedCompany
        body.oldArea.country = this.selectedCountry
        body.newArea.country = value
      } else if (target === 'region') {
        body.oldArea.company = this.selectedCompany
        body.newArea.company = this.selectedCompany
        body.oldArea.country = this.selectedCountry
        body.newArea.country = this.selectedCountry
        body.oldArea.region = this.selectedRegion
        body.newArea.region = value
      } else if (target === 'city') {
        body.oldArea.company = this.selectedCompany
        body.newArea.company = this.selectedCompany
        body.oldArea.country = this.selectedCountry
        body.newArea.country = this.selectedCountry
        body.oldArea.region = this.selectedRegion
        body.newArea.region = this.selectedRegion
        body.oldArea.city = this.selectedCity
        body.newArea.city = value
      }
      this.$utils.callAxiosWithBody('put', url, body, config).then(res => {
        EventBus.$emit('messageAlert', this.$t(res.data.responseMessage))
        if (target === 'company') this.selectedCompany = null
        else if (target === 'country') this.selectedCountry = null
        else if (target === 'region') this.selectedRegion = null
        else if (target === 'city') this.selectedCity = null
        this.getArea()
        EventBus.$emit('setManagedStores')
      })
    },
    deleteArea (target) {
      const url = '/api/common/area'
      const config = {
        data: {
          company: '',
          country: '',
          region: '',
          city: ''
        }
      }
      if (target === 'company') {
        config.data.company = this.selectedCompany
      } else if (target === 'country') {
        config.data.company = this.selectedCompany
        config.data.country = this.selectedCountry
      } else if (target === 'region') {
        config.data.company = this.selectedCompany
        config.data.country = this.selectedCountry
        config.data.region = this.selectedRegion
      } else if (target === 'city') {
        config.data.company = this.selectedCompany
        config.data.country = this.selectedCountry
        config.data.region = this.selectedRegion
        config.data.city = this.selectedCity
      }

      this.$utils.callAxios('delete', url, config).then(res => {
        EventBus.$emit('messageAlert', this.$t(res.data.responseMessage))
        if (target === 'company') this.selectedCompany = null
        else if (target === 'country') this.selectedCountry = null
        else if (target === 'region') this.selectedRegion = null
        else if (target === 'city') this.selectedCity = null
        this.getArea()
      })
    }
  },
  mounted () {
    const serverType = this.$store.getters['auth/GET_USER'].serverType
    if (serverType === 'SINGLE') {
      // serverType === 'SINGLE' 이면 Area Group Management 숨김
      this.SingleUser = true
    }
    if (serverType) {
      this.$store.dispatch('auth/getDisabledBtn', '9100').then(flag => {
        this.btnDisabledAlertSetting = flag
      })
    }
    this.$store.dispatch('auth/getDisabledBtn', '9101').then(flag => {
      this.btnDisabledAreaSetting = flag
    })

    // 상단 공통 팝업 & 자동완성기능 사용유무
    EventBus.$emit('enableSelectedStores', false)
    this.aliveInterval = this.$store.getters['auth/GET_INTERVAL']
    this.getAlertSetting()
    this.getCompany()
    // this.getArea()
  }
}
</script>
<style scoped>
.hidden {
  display: none;
}
</style>
