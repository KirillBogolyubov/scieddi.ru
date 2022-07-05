<template>
  <div class="heading">
    <div v-if="leftLine" class="heading__line"></div>
    <div class="heading__header">
      <h2 :is="isMain ? 'h1' : 'h2'" class="heading__header-text">
        {{ heading }}
      </h2>
      <header-circle :count="count" />
    </div>
    <div v-if="description" class="heading__description">
      <div class="heading__description-text">{{ description }}</div>
    </div>
    <div v-if="isMain" class="heading__line"></div>
    <div class="heading__content-nothing"></div>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  import HeaderCircle from '~/components/atoms/HeaderCircle.vue';

  export default defineComponent({
    name: 'HeaderH2',
    components: {
      HeaderCircle,
    },
    props: {
      heading: {
        type: String,
        require: true,
      },
      isMain: {
        type: Boolean,
      },
      description: String,
      count: {
        type: Number,
      },
      leftLine: Boolean,
    },
  });
</script>

<style lang="scss" scoped>
  @import './css/settings';

  .heading {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    grid-row-gap: map-get($units, xsmall) * 2;
    padding-bottom: map-get($units, xsmall) * 30;
    padding-top: map-get($units, xsmall) * 30;

    &__line {
      align-self: center;
      background-color: $color-header-h2-line-color;
      display: flex;
      height: map-get($units, xsmall) * 1;
    }

    &__header {
      display: flex;
      grid-column: 2;
      justify-content: center;
      padding-left: map-get($units, xsmall) * 10;
      padding-right: map-get($units, xsmall) * 10;

      & h2 {
        font-size: map-get($units, xsmall) * 30;
      }

      & h1 {
        font-size: map-get($units, xsmall) * 40;
      }

      &-text {
        color: $color-header-h2-text-color;
        display: flex;
        font-family: 'Play', sans-serif;
        font-weight: 700;
        line-height: map-get($units, xsmall) * 34;
        text-align: center;
        text-transform: uppercase;
      }
    }

    &__description {
      display: flex;
      grid-row: 2;
      grid-column: 2;
      justify-content: center;
      padding-bottom: map-get($units, xsmall) * 20;

      &-text {
        align-self: center;
        border: $color-header-h2-description-border-color
          map-get($units, xsmall) * 1 solid;
        border-radius: map-get($units, xsmall) * 4;
        color: $color-header-h2-description-text-color;
        font-size: map-get($units, xsmall) * 12;
        font-weight: 400;
        line-height: map-get($units, xsmall) * 20;
        padding: map-get($units, xsmall) * 5 map-get($units, xsmall) * 20;
        text-transform: uppercase;
        width: auto;
      }
    }
  }

  @include breakpoint(small) {
    .heading {
      grid-row-gap: map-get($units, small) * 2;
      padding-bottom: map-get($units, small) * 40;
      padding-top: map-get($units, small) * 30;

      &__line {
        height: map-get($units, small) * 1;
      }

      &__header {
        padding-left: map-get($units, small) * 30;
        padding-right: map-get($units, small) * 30;

        & h2 {
          font-size: map-get($units, small) * 35;
        }

        & h1 {
          font-size: map-get($units, small) * 40;
        }

        &-text {
          line-height: map-get($units, small) * 39;
        }
      }

      &__description {
        padding-bottom: map-get($units, small) * 20;

        &-text {
          border-width: map-get($units, small) * 1;
          border-radius: map-get($units, small) * 4;
          font-size: map-get($units, small) * 12;
          line-height: map-get($units, small) * 20;
          padding: map-get($units, small) * 5 map-get($units, small) * 20;
        }
      }
    }
  }

  @include breakpoint(medium) {
    .heading {
      grid-row-gap: map-get($units, medium) * 2;
      padding-bottom: map-get($units, medium) * 50;
      padding-top: map-get($units, medium) * 30;

      &__line {
        height: map-get($units, medium) * 1;
      }

      &__header {
        padding-left: map-get($units, medium) * 50;
        padding-right: map-get($units, medium) * 50;

        & h2 {
          font-size: map-get($units, medium) * 35;
        }

        & h1 {
          font-size: map-get($units, medium) * 40;
        }

        &-text {
          line-height: map-get($units, medium) * 39;
        }
      }

      &__description {
        padding-bottom: map-get($units, medium) * 20;

        &-text {
          border-width: map-get($units, medium) * 1;
          border-radius: map-get($units, medium) * 4;
          font-size: map-get($units, medium) * 12;
          line-height: map-get($units, medium) * 20;
          padding: map-get($units, medium) * 5 map-get($units, medium) * 20;
        }
      }
    }
  }

  @include breakpoint(large) {
    .heading {
      padding-bottom: map-get($units, large) * 60;
      padding-top: map-get($units, large) * 30;

      &__line {
        height: map-get($units, large) * 1;
      }

      &__header {
        display: flex;
        padding-left: map-get($units, large) * 70;
        padding-right: map-get($units, large) * 70;

        & h2 {
          font-size: map-get($units, large) * 40;
        }

        & h1 {
          font-size: map-get($units, large) * 50;
        }

        &-text {
          line-height: map-get($units, large) * 45;
        }
      }

      &__description {
        display: flex;
        grid-row: initial;
        grid-column: initial;
        justify-content: flex-start;
        padding-bottom: initial;

        &-text {
          border-width: map-get($units, large) * 1;
          border-radius: map-get($units, large) * 4;
          font-size: map-get($units, large) * 12;
          line-height: map-get($units, large) * 20;
          padding: map-get($units, large) * 5 map-get($units, large) * 15;
        }
      }
    }
  }

  @include breakpoint(xlarge) {
    .heading {
      padding-bottom: map-get($units, xlarge) * 70;
      padding-top: map-get($units, xlarge) * 30;

      &__line {
        height: map-get($units, xlarge) * 1;
      }

      &__header {
        padding-left: map-get($units, xlarge) * 90;
        padding-right: map-get($units, xlarge) * 90;

        & h2 {
          font-size: map-get($units, xlarge) * 45;
        }

        & h1 {
          font-size: map-get($units, xlarge) * 50;
        }

        &-text {
          line-height: map-get($units, xlarge) * 50;
        }
      }

      &__description {
        &-text {
          border-width: map-get($units, xlarge) * 1;
          border-radius: map-get($units, xlarge) * 4;
          font-size: map-get($units, xlarge) * 12;
          line-height: map-get($units, xlarge) * 20;
          padding: map-get($units, xlarge) * 5 map-get($units, xlarge) * 15;
        }
      }
    }
  }

  @include breakpoint(xxlarge) {
    .heading {
      padding-bottom: map-get($units, xxlarge) * 80;
      padding-top: map-get($units, xxlarge) * 30;

      &__line {
        height: map-get($units, xxlarge) * 1;
      }

      &__header {
        padding-left: map-get($units, xxlarge) * 110;
        padding-right: map-get($units, xxlarge) * 110;

        & h2 {
          font-size: map-get($units, xxlarge) * 50;
        }

        & h1 {
          font-size: map-get($units, xxlarge) * 50;
        }

        &-text {
          line-height: map-get($units, xxlarge) * 65;
        }
      }

      &__description {
        &-text {
          border-width: map-get($units, xxlarge) * 1;
          border-radius: map-get($units, xxlarge) * 4;
          font-size: map-get($units, xxlarge) * 12;
          line-height: map-get($units, xxlarge) * 20;
          padding: map-get($units, xxlarge) * 5 map-get($units, xxlarge) * 15;
        }
      }
    }
  }
</style>
