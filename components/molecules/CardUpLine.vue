<template>
  <div class="card">
    <slot />
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    name: 'CardUpLine',
    props: {
      goal: {
        type: String,
        require: true,
      },
    },
    setup() {
      return {};
    },
  });
</script>

<style lang="scss" scoped>
  @import './css/settings';

  .card {
    display: flex;
    justify-content: center;
    align-items: center;
    color: $white-color;
    background-color: $dark-blue-color;
    width: 100%;
    border-radius: map-get($units, xsmall) * 5;
    border-top: map-get($units, xsmall) * 5 solid $secondary-color;
    margin-bottom: map-get($units, xsmall) * 1;
    padding: map-get($units, xsmall) * 20;
    font-size: map-get($units, xsmall) * 16;
    font-weight: 400;
    line-height: map-get($units, xsmall) * 30;
    text-align: center;
  }

  @include breakpoint(small) {
    .card {
      border-radius: map-get($units, small) * 5;
      border-top: map-get($units, small) * 5 solid $secondary-color;
      margin-bottom: map-get($units, small) * 1;
      padding: map-get($units, small) * 20;
      font-size: map-get($units, small) * 16;
      line-height: map-get($units, small) * 30;
    }
  }

  @include breakpoint(medium) {
    .card {
      border-radius: map-get($units, medium) * 5;
      border-top: map-get($units, medium) * 5 solid $secondary-color;
      margin-bottom: map-get($units, medium) * 1;
      padding: map-get($units, medium) * 20;
      font-size: map-get($units, medium) * 20;
      line-height: map-get($units, medium) * 30;
    }
  }

  @include breakpoint(large) {
    .card {
      border-radius: map-get($units, large) * 5;
      border-top: map-get($units, large) * 5 solid $secondary-color;
      margin-bottom: map-get($units, large) * 1;
      padding: map-get($units, large) * 20;
      font-size: map-get($units, large) * 20;
      line-height: map-get($units, large) * 30;
    }
  }

  @include breakpoint(xlarge) {
    .card {
      border-radius: map-get($units, xlarge) * 5;
      border-top: map-get($units, xlarge) * 5 solid $secondary-color;
      margin-bottom: map-get($units, xlarge) * 1;
      padding: map-get($units, xlarge) * 20;
      font-size: map-get($units, xlarge) * 22;
      line-height: map-get($units, xlarge) * 30;
    }
  }

  @include breakpoint(xxlarge) {
    .card {
      border-radius: map-get($units, xxlarge) * 5;
      border-top: map-get($units, xxlarge) * 5 solid $secondary-color;
      margin-bottom: map-get($units, xxlarge) * 1;
      padding: map-get($units, xxlarge) * 20;
      font-size: map-get($units, xxlarge) * 22;
      line-height: map-get($units, xxlarge) * 30;
    }
  }
</style>
