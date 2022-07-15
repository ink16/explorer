<template>
  <b-container class="pb-3">
    <span class="float-md-left d-none d-md-block d-md-inline-block">
      <b-img
        src="/logos/humans.svg"
        alt="humans logo"
        width="40"
      />
    </span>

    <span class="float-md-right d-none d-md-block d-md-inline-block">
      <b-link
        class="mr-50 "
        href="agoric"
        target="_blank"
      >Summary</b-link>
      <b-link
        class="ml-50 mr-50 "
        href="#"
        target="_blank"
      >Blocks</b-link>
      <b-link
        class="ml-50 mr-50 "
        href="#"
        target="_blank"
      >Staking</b-link>
      <b-link
        class="ml-50 "
        href="#"
        target="_blank"
      >Governance</b-link>
      <b-link
        class="ml-50 "
        href="#"
        target="_blank"
      >Uptime</b-link>
    </span>

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
    BLink, BContainer, BRow, BCol, BImg,
  },
  directives: {
    'b-popover': VBPopover,
    Ripple,
  },
}
</script>
