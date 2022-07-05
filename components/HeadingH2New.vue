<template>
  <div class="heading">
    <div class="heading__line"></div>
    <h2 class="heading__header">{{ heading }}</h2>
    <div class="heading__nothing"></div>

    <div class="heading__description">
      <div v-if="description">{{ description }}</div>
    </div>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    name: 'HeadingH2',
    props: {
      heading: {
        type: String,
        require: true,
      },
      description: String,
    },
  });
</script>

<style lang="scss" scoped>
  @import '../css/settings';

  .heading {
    display: grid;
    grid-template-areas:
      'line header nothing'
      'descr descr descr';
    grid-template-columns: 20% 60% 20%;
    align-items: center;
    margin: map-get($units, xsmall) * 63 0;
    width: 100%;

    &__line {
      grid-area: line;
      background-color: $color-header-line;
      height: map-get($units, xsmall);
    }

    &__header {
      grid-area: header;
      display: inline-block;
      font-family: 'Play', sans-serif;
      color: $color-header;
      font-size: map-get($units, xsmall) * 30;
      line-height: map-get($units, xsmall) * 34.71;
      max-width: map-get($units, xsmall) * 360;
      text-transform: uppercase;
      text-align: center;
      width: auto;
    }

    &__nothing {
      grid-area: nothing;
      background-color: transparent;
      height: map-get($units, xsmall);
    }

    &__description {
      grid-area: descr;
      text-align: center;
      width: 100%;

      & div {
        color: $color-header;
        display: inline-block;
        font-size: map-get($units, xsmall) * 12;
        border: map-get($units, xsmall) solid $color-header-line;
        border-radius: map-get($units, xsmall) * 4.6;
        padding: map-get($units, xsmall) * 8 map-get($units, xsmall) * 10;
        margin: map-get($units, xsmall) * 30 auto auto;
        max-width: map-get($units, xsmall) * 320;
        width: auto;
      }
    }
  }

  @include breakpoint(small) {
    .heading {
      grid-template-columns: 25% 50% 25%;
      margin: map-get($units, small) * 63 0;

      &__line {
        height: map-get($units, small);
        min-width: map-get($units, small);
      }

      &__header {
        font-size: map-get($units, small) * 35;
        line-height: map-get($units, small) * 40;
        max-width: map-get($units, small) * 420;
      }

      &__description {
        & div {
          font-size: map-get($units, small) * 14;
          border-width: map-get($units, small);
          border-radius: map-get($units, small) * 4.6;
          padding: map-get($units, small) * 12 map-get($units, small) * 20;
          margin: map-get($units, small) * 40 auto auto;
          max-width: map-get($units, small) * 400;
        }
      }
    }
  }

  @include breakpoint(medium) {
    .heading {
      grid-template-columns: 30% 40% 30%;
      margin: map-get($units, medium) * 63 0;

      &__line {
        height: map-get($units, medium);
        min-width: map-get($units, medium);
      }

      &__header {
        //padding: 0 map-get($units, medium) * 50;
        font-size: map-get($units, medium) * 35;
        line-height: map-get($units, medium) * 40;
        max-width: map-get($units, medium) * 460;
      }

      &__description {
        & div {
          font-size: map-get($units, medium) * 14;
          border-width: map-get($units, medium);
          border-radius: map-get($units, medium) * 4.6;
          padding: map-get($units, medium) * 12 map-get($units, medium) * 20;
          margin: map-get($units, medium) * 40 auto auto;
          max-width: map-get($units, medium) * 460;
        }
      }
    }
  }

  @include breakpoint(large) {
    .heading {
      grid-template-areas: 'line header descr';
      grid-template-columns: 38% 25% 37%;
      margin: map-get($units, large) * 63 0;

      &__line {
        height: map-get($units, large);
        min-width: map-get($units, large);
      }

      &__header {
        margin: auto;
        font-size: map-get($units, large) * 35;
        line-height: map-get($units, large) * 40;
        max-width: map-get($units, large) * 460;
      }

      &__nothing {
        display: none;
      }

      &__description {
        flex-grow: 23;
        text-align: left;
        width: auto;

        & div {
          font-size: map-get($units, large) * 14;
          border-width: map-get($units, large);
          border-radius: map-get($units, large) * 4.6;
          padding: map-get($units, large) * 12 map-get($units, large) * 20;
          margin: 0;
          max-width: map-get($units, large) * 460;
        }
      }
    }
  }

  @include breakpoint(xlarge) {
    .heading {
      grid-template-columns: 40% 20% 40%;
      margin: map-get($units, xlarge) * 63 0;

      &__line {
        height: map-get($units, xlarge);
        min-width: map-get($units, xlarge);
      }

      &__header {
        font-size: map-get($units, xlarge) * 35;
        line-height: map-get($units, xlarge) * 40;
        max-width: map-get($units, xlarge) * 460;
      }

      &__description {
        & div {
          font-size: map-get($units, xlarge) * 14;
          border-width: map-get($units, xlarge);
          border-radius: map-get($units, xlarge) * 4.6;
          padding: map-get($units, xlarge) * 12 map-get($units, xlarge) * 20;
          max-width: map-get($units, xlarge) * 460;
        }
      }
    }
  }

  @include breakpoint(xxlarge) {
    .heading {
      grid-template-columns: 42% 15% 43%;
      margin: map-get($units, xxlarge) * 63 0;

      &__line {
        height: map-get($units, xxlarge);
        min-width: map-get($units, xxlarge);
      }

      &__header {
        font-size: map-get($units, xxlarge) * 35;
        line-height: map-get($units, xxlarge) * 40;
        max-width: map-get($units, xxlarge) * 460;
      }

      &__description {
        & div {
          font-size: map-get($units, xxlarge) * 14;
          border-width: map-get($units, xxlarge);
          border-radius: map-get($units, xxlarge) * 4.6;
          padding: map-get($units, xxlarge) * 12 map-get($units, xxlarge) * 20;
          max-width: map-get($units, xxlarge) * 460;
        }
      }
    }
  }
</style>
