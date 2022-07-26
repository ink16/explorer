<template>
  <b-container class="pb-1">
    <div class="d-flex justify-content-between">
      <div class="d-none d-md-block d-md-inline-block">
        <b-img
          src="/logos/humans.svg"
          alt="humans logo"
          width=""
        />
      </div>
      <div class="d-flex flex-column justify-content-center align-items-center">
        <div class="d-flex">
          <b-link
            class="mr-50"
            href="devnet"
            target="_blank"
          >Summary</b-link>
          <b-link
            class="ml-50 mr-50"
            href="devnet/blocks"
            target="_blank"
          >Blocks</b-link>
          <b-link
            class="ml-50 mr-50"
            href="devnet/staking"
            target="_blank"
          >Staking</b-link>
          <b-link
            class="ml-50"
            href="devnet/governance"
            target="_blank"
          >Governance</b-link>
          <b-link
            class="ml-50"
            href="devnet/uptime"
            target="_blank"
          >Uptime</b-link>
        </div>
        <div class="d-flex">
          <b-link
            class="ml-50 mr-50"
            href="#"
            target="_blank"
          ><feather-icon
            icon="GithubIcon"
            size="16"
          /> Github</b-link>
          <b-link
            class="mr-50"
            href="agoric"
            target="_blank"
          >Discord</b-link>
          <b-link
            class="ml-50 mr-50"
            href="#"
            target="_blank"
          ><feather-icon
            icon="TwitterIcon"
            size="16"
          /> Twitter</b-link>

        </div>
      </div>
    </div>
  </b-container>
</template>

<script>
import {
  BLink, VBPopover, BContainer, BRow, BCol, BImg,
} from 'bootstrap-vue'
import Ripple from 'vue-ripple-directive'

export default {
  name: 'AppFooter',
  components: {
    BLink,
    BContainer,
    BRow,
    BCol,
    BImg,
  },
  directives: {
    'b-popover': VBPopover,
    Ripple,
  },
}
</script>
