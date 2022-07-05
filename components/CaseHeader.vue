<template>
  <div class="case-header" :class="{ invisible: !imageUrl }">
    <div class="case-header__image">
      <img v-if="imageUrl" class="image" :src="imageUrl" />
    </div>
    <div class="case-header__header">
      <h1 class="header">
        <small class="header__sub">{{ subheader }}</small>
        <strong class="header__main">{{ header }}</strong>
      </h1>
    </div>
    <div class="case-header__description">
      <slot name="description" />
    </div>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    name: 'CaseHeader',
    props: {
      imageUrl: {
        type: String,
      },
      header: {
        type: String,
        required: true,
      },
      subheader: {
        type: String,
        required: true,
      },
    },
  });
</script>

<style lang="scss" scoped>
  @import '../css/settings';

  .case-header {
    display: grid;
    grid-template-areas: 'case-header-image' 'case-header-header' 'case-header-description';
    padding-bottom: map-get($units, xsmall) * 41;
    width: 100%;

    &__image {
      grid-area: case-header-image;
    }

    &__header {
      grid-area: case-header-header;
    }

    &__description {
      grid-area: case-header-description;
    }
  }

  .image {
    width: 100%;
  }

  .header {
    display: grid;
    grid-template-rows: auto auto;
    grid-row-gap: map-get($units, xsmall) * 18;
    text-transform: uppercase;
    text-align: center;
    margin: map-get($units, xsmall) * 40.95 0;
    overflow: hidden;
    width: 100%;
    justify-items: start;

    &__main {
      display: inline-block;
      font-size: map-get($units, xsmall) * 22;
      line-height: map-get($units, xsmall) * 30;
      justify-items: left;
      text-align: left;
    }

    &__sub {
      display: inline-block;
      font-size: map-get($units, xsmall) * 12;
      line-height: map-get($units, xsmall) * 21;
      font-weight: 300;
      border: map-get($units, xsmall) solid $secondary-color;
      border-radius: map-get($units, xsmall) * 4.61821;
      padding: map-get($units, xsmall) * 14;
      width: map-get($units, xsmall) * 235;
    }
  }

  @include breakpoint(small) {
    .case-header {
      padding-bottom: map-get($units, small) * 41;

      &__image {
        padding: 0 map-get($units, small) * 138;
      }
    }

    .header {
      grid-row-gap: map-get($units, small) * 18;
      margin: map-get($units, small) * 40.95 0;
      justify-items: start;

      &__main {
        font-size: map-get($units, small) * 28;
        line-height: map-get($units, small) * 36;
      }

      &__sub {
        font-size: map-get($units, small) * 12;
        line-height: map-get($units, small) * 21;
        border-width: map-get($units, small);
        border-radius: map-get($units, small) * 4.61821;
        padding: map-get($units, small) * 14;
        width: auto;
      }
    }
  }

  @include breakpoint(medium) {
    .case-header {
      //grid-template-areas: 'case-header-image case-header-header' 'case-header-description case-header-description';
      //grid-template-columns: map-get($units, medium) * 310 1fr;
      grid-column-gap: map-get($units, medium) * 72;
      padding-bottom: map-get($units, medium) * 41;

      &__image {
        padding: 0;
        //width: map-get($units, medium) * 310;
        width: 50%;
        justify-self: center;
      }
    }

    .header {
      grid-row-gap: map-get($units, medium) * 18;
      margin: 0;
      justify-items: start;
      grid-column: 1;
      padding: map-get($units, medium) * 36 0 0;

      &__main {
        font-size: map-get($units, medium) * 30;
        line-height: map-get($units, medium) * 36.95;
      }

      &__sub {
        font-size: map-get($units, medium) * 12;
        line-height: map-get($units, medium) * 21;
        border-width: map-get($units, medium);
        border-radius: map-get($units, medium) * 4.61821;
        padding: map-get($units, medium) * 14;
      }
    }
  }

  @include breakpoint(large) {
    .case-header {
      grid-template-areas: 'case-header-image case-header-header' 'case-header-image case-header-description';
      grid-template-columns: map-get($units, large) * 310 1fr;
      grid-column-gap: map-get($units, large) * 60;
      padding-bottom: map-get($units, large) * 41;

      &.invisible {
        grid-template-areas: 'case-header-header' 'case-header-description';
        grid-template-columns: 1fr;
        grid-column-gap: 0;

        .content-line {
          width: 70%;
        }
      }

      &__image {
        display: flex;
        align-items: center;
        padding-top: map-get($units, large) * 40;
        //width: map-get($units, medium) * 310;
        width: 100%;
      }
    }

    .header {
      //display: block;
      grid-row-gap: map-get($units, large) * 18;
      text-align: left;
      justify-items: start;

      &__main {
        font-size: map-get($units, large) * 32;
        line-height: map-get($units, large) * 45;
        padding-top: map-get($units, large) * 29;
      }

      &__sub {
        display: block;
        font-size: map-get($units, large) * 12;
        line-height: map-get($units, large) * 21;
        border-width: map-get($units, large);
        border-radius: map-get($units, large) * 4.61821;
        padding: map-get($units, large) * 14;
      }
    }
  }

  @include breakpoint(xlarge) {
    .case-header {
      grid-template-columns: map-get($units, xlarge) * 480 1fr;
      grid-column-gap: map-get($units, xlarge) * 100;
      padding-bottom: 0;

      &__image {
        padding-top: unset;
        display: flex;
        align-items: center;
      }

      &__description {
        padding-bottom: map-get($units, xlarge) * 30;
      }
    }

    .header {
      grid-row-gap: map-get($units, xlarge) * 18;

      &__main {
        //display: block;
        font-size: map-get($units, xlarge) * 35;
        line-height: map-get($units, xlarge) * 45;
        padding-top: map-get($units, xlarge) * 29;
      }

      &__sub {
        font-size: map-get($units, xlarge) * 12;
        line-height: map-get($units, xlarge) * 21;
        border-width: map-get($units, xlarge);
        border-radius: map-get($units, xlarge) * 4.61821;
        padding: map-get($units, xlarge) * 14;
      }
    }
  }

  @include breakpoint(xxlarge) {
    .case-header {
      grid-template-columns: map-get($units, xxlarge) * 664 * 0.7 1fr;
      grid-column-gap: map-get($units, xxlarge) * 227 * 0.5;
      grid-row-gap: map-get($units, xxlarge) * 30 * 0.7;

      &__description {
        padding-bottom: map-get($units, xxlarge) * 10 * 0.7;
      }
    }

    .header {
      grid-row-gap: map-get($units, xxlarge) * 18;

      &__main {
        //display: block;
        font-size: map-get($units, xxlarge) * 35;
        line-height: map-get($units, xxlarge) * 45;
        padding-top: map-get($units, xxlarge) * 29;
      }

      &__sub {
        font-size: map-get($units, xxlarge) * 12;
        line-height: map-get($units, xxlarge) * 21;
        border-width: map-get($units, xxlarge);
        border-radius: map-get($units, xxlarge) * 4.61821;
        padding: map-get($units, xxlarge) * 14;
      }
    }
  }
</style>
