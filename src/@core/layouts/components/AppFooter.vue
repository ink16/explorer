<template>
  <h2 class="clearfix mb-0">
    <span class="float-md-left d-none d-md-block d-md-inline-block mt-25">
      <b-link
        class="mr-25 font-weight-bolder"
        href="#"
        target="_blank"
      >Humans.ai</b-link>
      | Explorer
    </span>

    <router-link
      v-ripple.400="'rgba(113, 102, 240, 0.15)'"
      class="float-md-right"
      to="/coffee"
    >Buy me a cup of coffee.
      <span
        v-ripple.400="'rgba(113, 102, 240, 0.15)'"
        variant="outline-primary"
      >
        <feather-icon
          icon="HeartIcon"
          size="21"
          class="text-danger stroke-current"
        />
      </span>
    </router-link>
  </h2>
</template>

<script>
import { BLink, VBPopover } from 'bootstrap-vue'
import Ripple from 'vue-ripple-directive'

export default {
  name: 'AppFooter',
  components: {
    BLink,
  },
  directives: {
    'b-popover': VBPopover,
    Ripple,
  },
}
</script>
