<template>
  <!-- Nav Menu Toggler deleted -->

  <!-- Left Col -->

  <!-- <dark-Toggler class="d-none d-lg-block" /> -->
  <!-- Right Col -->

  <!--add  fixed="top" for sticky navbar-->
  <b-navbar
    toggleable="lg"
    class="header-navbar my-2 navbar-expand-lg"
  >

    <div class="navbar-container d-flex content justify-content-between">

      <div class="d-flex justify-content-start">
        <b-navbar-toggle
          target="nav-collapse"
          class="mr-auto base"
          type="base"
        />
        <b-link
          :to="{path:'/devnet'}"
          style="padding-top: 11px;"
        >
          <b-img
            src="/logos/humans.svg"
            alt="humans logo"
            class="d-none d-xl-flex img-fluid"
          />
        </b-link>
        <div class="d-flex align-items-center justify-content-center px-1">
          <b-link
            :to="{path:'/devnet'}"
          >
            <b-img
              src="/logos/humans-mobile.svg"
              alt="humans logo"
              class="d-xl-none"
            />
          </b-link></div>
      </div>

      <!-- Left Col -->
      <!-- Middle Col-->
      <b-collapse
        id="nav-collapse"
        is-nav
      >
        <!-- Nav Menu Toggler -->
        <div class="d-flex flex-column flex-lg-row justify-content-between w-100">
          <b-navbar-nav class="d-flex flex-column flex-lg-row align-items-start">
            <b-nav-item
              class="app-nav-link mr-1"
              href="/devnet"
              :class="{active: $route.name==='summary'}"
            >
              Summary
            </b-nav-item>
            <b-nav-item
              class="app-nav-link mr-1"
              href="/devnet/blocks"
              :class="{active: $route.name==='blocks'}"
            >
              Blocks
            </b-nav-item>
            <b-nav-item
              class="app-nav-link mr-1"
              href="/devnet/staking"
              :class="{active: $route.name==='staking'}"
            >
              Staking
            </b-nav-item>
            <b-nav-item
              class="app-nav-link mr-1"
              href="/devnet/governance"
              :class="{active: $route.name==='governance'}"
            >
              Governance
            </b-nav-item>
            <b-nav-item
              class="app-nav-link mr-1"
              href="/devnet/uptime"
              :class="{active: $route.name==='uptime'}"
            >
              Uptime
            </b-nav-item>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <!--<b-navbar-nav class="ml-auto">
          x
        </b-navbar-nav>-->
          <!-- Right Col -->
          <b-navbar-nav class="nav align-items-center d-flex flex-nowrap">
            <search-bar class="d-none d-lg-flex" />
            <b-dropdown
              class="ml-1"
              variant="link"
              no-caret
              toggle-class="p-0"
              right
            >

              <template #button-content>
                <b-button
                  v-ripple.400="'rgba(255, 255, 255, 0.15)'"
                  variant="primary"
                  class="btn-icon"
                >
                  <feather-icon icon="KeyIcon" />
                  {{ walletName }}
                </b-button>
              </template>

              <b-dropdown-item
                v-for="(item,k) in accounts"
                :key="k"
                :disabled="!item.address"
                :to="`/${selected_chain.chain_name}/account/${item.address.addr}`"
                @click="updateDefaultWallet(item.wallet)"
              >
                <div class="d-flex flex-column">
                  <span class="font-weight-bolder">{{ item.wallet }}
                    <b-avatar
                      v-if="item.wallet===walletName"
                      variant="success"
                      size="sm"
                    >
                      <feather-icon icon="CheckIcon" />
                    </b-avatar>
                  </span>
                  <small>{{ item.address ? formatAddr(item.address.addr) : `Not available on ${selected_chain.chain_name}` }}</small>
                </div>
              </b-dropdown-item>
              <b-dropdown-divider />
              <b-dropdown-item to="/wallet/import">
                <feather-icon
                  icon="PlusIcon"
                  size="16"
                />
                <span class="align-middle ml-50">Import Address</span>
              </b-dropdown-item>
              <b-dropdown-divider />

              <b-dropdown-item :to="{ name: 'accounts' }">
                <feather-icon
                  icon="KeyIcon"
                  size="16"
                />
                <span class="align-middle ml-50">Accounts</span>
              </b-dropdown-item>

              <b-dropdown-item :to="{ name: 'delegations' }">
                <feather-icon
                  icon="BookOpenIcon"
                  size="16"
                />
                <span class="align-middle ml-50">My Delegations</span>
              </b-dropdown-item>

              <b-dropdown-item :to="`/${selected_chain.chain_name}/uptime/my`">
                <feather-icon
                  icon="AirplayIcon"
                  size="16"
                />
                <span class="align-middle ml-50">My Validators</span>
              </b-dropdown-item>

              <b-dropdown-item :to="`/wallet/votes`">
                <feather-icon
                  icon="PocketIcon"
                  size="16"
                />
                <span class="align-middle ml-50">My Votes</span>
              </b-dropdown-item>

              <b-dropdown-item :to="`/wallet/transactions`">
                <feather-icon
                  icon="LayersIcon"
                  size="16"
                />
                <span class="align-middle ml-50">My Transactions</span>
              </b-dropdown-item>
            </b-dropdown>
          </b-navbar-nav>
        </div>
      </b-collapse>
      <div class="d-flex align-items-center justify-content-end ml-auto">
        <search-bar class="d-lg-none" />
      </div>
      <!-- <dark-Toggler class="d-none d-lg-block" /> -->
    </div>
  </b-navbar>

</template>

<script>
import {
  BNavbarNav, BAvatar, VBTooltip, BButton, BDropdown, BDropdownItem, BDropdownDivider, BCollapse, BNavbarToggle, BNavbarBrand, BNavItem, BNavForm, BNavbar, BImg, BLink,
} from 'bootstrap-vue'
import Ripple from 'vue-ripple-directive'
import DarkToggler from '@core/layouts/components/app-navbar/components/DarkToggler.vue'
import Locale from '@core/layouts/components/app-navbar/components/Locale.vue'
import SearchBar from '@core/layouts/components/app-navbar/components/SearchBar.vue'
// import CartDropdown from '@core/layouts/components/app-navbar/components/CartDropdown.vue'
import { getLocalAccounts, timeIn, toDay } from '@/libs/utils'
// import UserDropdown from '@core/layouts/components/app-navbar/components/UserDropdown.vue'

export default {
  components: {
    BLink,
    BImg,
    BNavbar,
    BNavForm,
    BCollapse,
    BNavbarToggle,
    BNavbarNav,
    BNavbarBrand,
    BNavItem,
    BAvatar,
    BButton,
    BDropdown,
    BDropdownItem,
    BDropdownDivider,

    // Navbar Components
    DarkToggler,
    Locale,
    SearchBar,
    // CartDropdown,
    // UserDropdown,
  },
  directives: {
    'b-tooltip': VBTooltip,
    Ripple,
  },
  props: {
    toggleVerticalMenuActive: {
      type: Function,
      default: () => {},
    },
  },
  data() {
    return {
      variant: 'success',
      tips: 'Synced',
      index: 0,
      chainid: '',
    }
  },
  computed: {
    walletName() {
      const key = this.$store?.state?.chains?.defaultWallet
      return key || 'Wallet'
    },
    selected_chain() {
      this.block()
      return this.$store.state.chains.selected
    },
    chainVariant() {
      return this.variant
    },
    currentApi() {
      return this.index + 1 > this.apiOptions.length ? this.apiOptions[0] : this.apiOptions[this.index]
    },
    apiOptions() {
      const conf = this.$store.state.chains.selected
      if (Array.isArray(conf.api)) {
        return conf.api
      }
      return [conf.api]
    },
    accounts() {
      let accounts = getLocalAccounts() || {}
      accounts = Object.entries(accounts).map(v => ({ wallet: v[0], address: v[1].address.find(x => x.chain === this.selected_chain.chain_name) }))

      if (accounts.length > 0) {
        this.updateDefaultWallet(accounts[0].wallet)
      }
      return accounts.filter(x => x.address)
    },
  },
  mounted() {},
  methods: {
    formatAddr(v) {
      return v.substring(0, 10).concat('...', v.substring(v.length - 10))
    },
    updateDefaultWallet(v) {
      this.$store.commit('setDefaultWallet', v)
    },
    change(v) {
      this.index = v
      const conf = this.$store.state.chains.selected
      localStorage.setItem(`${conf.chain_name}-api-index`, v)
      window.location.reload()
    },
    block() {
      const conf = this.$store.state.chains.selected
      const s = localStorage.getItem(`${conf.chain_name}-api-index`) || 0
      this.index = Number(s)
      this.$store.commit('setHeight', 0)
      this.$http.getLatestBlock().then(block => {
        this.chainid = block.block.header.chain_id
        this.$store.commit('setHeight', Number(block.block.header.height))
        if (timeIn(block.block.header.time, 1, 'm')) {
          this.variant = 'danger'
          this.tips = `Halted ${toDay(block.block.header.time, 'from')}, Height: ${this.$store.state.chains.height} `
        } else {
          this.variant = 'success'
          this.tips = 'Synced'
        }
      })
    },
  },
}
</script>
