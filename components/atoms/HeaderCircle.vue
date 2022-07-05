<template>
  <div v-if="count" class="circle">
    <div class="circle__num">{{ count }}</div>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    name: 'HeaderCircle',
    props: {
      count: {
        type: Number,
      },
    },
  });
</script>

<style lang="scss" scoped>
  @import './css/settings';

  .circle {
    color: $color-header-circle-text-color;
    font-size: map-get($units, xsmall) * 13;
    line-height: map-get($units, xsmall) * 61;
    padding-left: map-get($units, xsmall) * 5;

    &__num {
      align-items: center;
      background-color: $color-header-circle-background-color;
      border-radius: 50%;
      display: flex;
      height: map-get($units, xsmall) * 24;
      justify-content: center;
      width: map-get($units, xsmall) * 24;
    }
  }

  @include breakpoint(small) {
    .circle {
      font-size: map-get($units, small) * 13;
      line-height: map-get($units, small) * 61;
      padding-left: map-get($units, small) * 5;

      &__num {
        height: map-get($units, small) * 24;
        width: map-get($units, small) * 24;
      }
    }
  }

  @include breakpoint(medium) {
    .circle {
      font-size: map-get($units, medium) * 13;
      line-height: map-get($units, medium) * 61;
      padding-left: map-get($units, medium) * 5;

      &__num {
        height: map-get($units, medium) * 24;
        width: map-get($units, medium) * 24;
      }
    }
  }

  @include breakpoint(large) {
    .circle {
      font-size: map-get($units, large) * 13;
      line-height: map-get($units, large) * 61;
      padding-left: map-get($units, large) * 5;

      &__num {
        height: map-get($units, large) * 24;
        width: map-get($units, large) * 24;
      }
    }
  }

  @include breakpoint(xlarge) {
    .circle {
      font-size: map-get($units, xlarge) * 13;
      line-height: map-get($units, xlarge) * 61;
      padding-left: map-get($units, xlarge) * 5;

      &__num {
        height: map-get($units, xlarge) * 24;
        width: map-get($units, xlarge) * 24;
      }
    }
  }

  @include breakpoint(xxlarge) {
    .circle {
      font-size: map-get($units, xxlarge) * 13;
      line-height: map-get($units, xxlarge) * 61;
      padding-left: map-get($units, xxlarge) * 5;

      &__num {
        height: map-get($units, xxlarge) * 24;
        width: map-get($units, xxlarge) * 24;
      }
    }
  }
</style>
