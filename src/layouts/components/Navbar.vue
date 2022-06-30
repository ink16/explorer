<template>
  <!-- Nav Menu Toggler deleted -->

  <!-- Left Col -->

  <!-- <dark-Toggler class="d-none d-lg-block" /> -->
  <!-- Right Col -->
  <b-navbar
    toggleable="lg"
    type="dark"
    :variant="info"
    class="header-navbar navbar navbar-shadow lg:align-items-center"
  >
    <b-container>
      <b-navbar-brand href="#">
        Explorer | Humans.ai
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse" />

      <b-collapse
        id="nav-collapse"
        is-nav
      >
        <b-navbar-nav class="mx-auto">
          <b-nav-item href="#">
            Summary
          </b-nav-item>
          <b-nav-item href="#">
            Blocks
          </b-nav-item>
          <b-nav-item href="#">
            Staking
          </b-nav-item>
          <b-nav-item href="#">
            Governance
          </b-nav-item>
          <b-nav-item href="#">
            Uptime
          </b-nav-item>
          <b-nav-item href="#">
            State Sync
          </b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-form-input
              size="sm"
              class="mr-sm-2"
              placeholder="Search"
            />
            <b-button
              size="sm"
              class="my-2 my-sm-0"
              type="submit"
            >
              Search
            </b-button>
          </b-nav-form>
        </b-navbar-nav>
      </b-collapse>
    </b-container>
  </b-navbar>

</template>

<script>
import {
  BNavbarNav, BMedia, BMediaAside, BAvatar, BMediaBody, VBTooltip, BButton, BDropdown, BDropdownItem, BDropdownDivider, BCollapse, BNavbarToggle, BNavbarBrand, BNavItem, BNavForm, BNavbar, BContainer,
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
    BContainer,
    BNavbar,
    BNavForm,
    BCollapse,
    BNavbarToggle,
    BNavbarNav,
    BNavbarBrand,
    BNavItem,
    BAvatar,
    BMedia,
    BMediaAside,
    BMediaBody,
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
