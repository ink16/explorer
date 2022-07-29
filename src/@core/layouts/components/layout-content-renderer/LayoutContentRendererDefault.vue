<template>
  <div
    class="container mt-5"
    :class="[{'show-overlay': $store.state.app.shallShowOverlay}, $route.meta.contentClass]"
  >
    <b-row class="align-items-center justify-content-center px-1">
      <b-col
        cols="12"
      >
        <div class="content-overlay" />
        <div class="header-navbar-shadow" />
        <div
          class="content-wrapper"
          :class="contentWidth === 'boxed' ? 'container p-0' : null"
        >
          <slot name="breadcrumb">
            <app-breadcrumb />
          </slot>
          <div class="content-body">
            <transition
              :name="routerTransition"
              mode="out-in"
            >
              <slot />
            </transition>

          </div>
        </div>
      </b-col>
    </b-row>
  </div></template>

<script>
import AppBreadcrumb from '@core/layouts/components/AppBreadcrumb.vue'
import useAppConfig from '@core/app-config/useAppConfig'
import { BRow, BContainer, BCol } from 'bootstrap-vue'

export default {
  components: {
    AppBreadcrumb,
    BRow,
    BContainer,
    BCol,
  },
  setup() {
    const { routerTransition, contentWidth } = useAppConfig()

    return {
      routerTransition, contentWidth,
    }
  },
}
</script>

<style>

</style>
