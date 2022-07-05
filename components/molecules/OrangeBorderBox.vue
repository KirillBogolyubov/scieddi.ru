<template>
  <div class="box">
    <div class="box__text">{{ content }}</div>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    name: 'OrangeBorderBox',
    props: {
      content: {
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
  @import '../../css/settings';

  .box {
    display: flex;
    justify-content: center;
    align-items: center;
    border: map-get($units, xsmall) solid $secondary-color;
    border-radius: map-get($units, xsmall) * 4.6;
    padding: map-get($units, xsmall) * 8 map-get($units, xsmall) * 20;
    text-align: center;
    width: auto;

    &__text {
      font-size: map-get($units, xsmall) * 12;
      line-height: map-get($units, xsmall) * 21;
    }
  }

  @include breakpoint(small) {
    .box {
      border: map-get($units, small) solid $secondary-color;
      border-radius: map-get($units, small) * 4.6;
      padding: map-get($units, small) * 8 map-get($units, small) * 20;

      &__text {
        font-size: map-get($units, small) * 12;
        line-height: map-get($units, small) * 21;
      }
    }
  }

  @include breakpoint(medium) {
    .box {
      border: map-get($units, medium) solid $secondary-color;
      border-radius: map-get($units, medium) * 4.6;
      padding: map-get($units, medium) * 8 map-get($units, medium) * 20;

      &__text {
        font-size: map-get($units, medium) * 12;
        line-height: map-get($units, medium) * 21;
      }
    }
  }

  @include breakpoint(large) {
    .box {
      border: map-get($units, large) solid $secondary-color;
      border-radius: map-get($units, large) * 4.6;
      padding: map-get($units, large) * 8 map-get($units, large) * 20;

      &__text {
        font-size: map-get($units, large) * 12;
        line-height: map-get($units, large) * 21;
      }
    }
  }

  @include breakpoint(xlarge) {
    .box {
      border: map-get($units, xlarge) solid $secondary-color;
      border-radius: map-get($units, xlarge) * 4.6;
      padding: map-get($units, xlarge) * 8 map-get($units, xlarge) * 20;

      &__text {
        font-size: map-get($units, xlarge) * 12;
        line-height: map-get($units, xlarge) * 21;
      }
    }
  }

  @include breakpoint(xxlarge) {
    .box {
      border: map-get($units, xxlarge) solid $secondary-color;
      border-radius: map-get($units, xxlarge) * 4.6;
      padding: map-get($units, xxlarge) * 8 map-get($units, xxlarge) * 20;

      &__text {
        font-size: map-get($units, xxlarge) * 12;
        line-height: map-get($units, xxlarge) * 21;
      }
    }
  }
</style>
