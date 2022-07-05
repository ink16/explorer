<template>
  <b-container>
    <span class="float-md-left d-none d-md-block d-md-inline-block">
      <b-link
        class="mr-25 font-weight-bolder"
        href="#"
        target="_blank"
      >Humans.ai</b-link>
      | Explorer
    </span>

    <span class="float-md-right d-none d-md-block d-md-inline-block">
      <b-link
        class="mr-50 font-weight-bolder"
        href="#"
        target="_blank"
      >About us</b-link>
      <b-link
        class="ml-50 mr-50 font-weight-bolder"
        href="#"
        target="_blank"
      >Contact</b-link>
      <b-link
        class="ml-50 mr-50 font-weight-bolder"
        href="#"
        target="_blank"
      >Jobs</b-link>
      <b-link
        class="ml-50 font-weight-bolder"
        href="#"
        target="_blank"
      >Press kit</b-link>
    </span>

  </b-container>
</template>

<script>
import {
  BLink, VBPopover, BContainer, BRow, BCol,
} from 'bootstrap-vue'
import Ripple from 'vue-ripple-directive'

export default {
  name: 'AppFooter',
  components: {
    BLink, BContainer, BRow, BCol,
  },
  directives: {
    'b-popover': VBPopover,
    Ripple,
  },
}
</script>
