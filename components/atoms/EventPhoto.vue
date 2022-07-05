<template>
  <div class="event-photo-container">
    <div class="slide">
      <smart-link
        :to="{
          name: 'events-id-preview',
          params: { id: $route.params.id },
          query: { number: num * 2 },
        }"
        :target="'_self'"
      >
        <smart-image
          class="slider__photo"
          is-show
          is-cover
          :src="src1"
          alt=""
        />
      </smart-link>
      <smart-link
        :to="{
          name: 'events-id-preview',
          params: { id: $route.params.id },
          query: { number: num * 2 + 1 },
        }"
        :target="'_self'"
      >
        <smart-image
          v-if="src2"
          class="slider__photo"
          is-show
          is-cover
          :src="src2"
          alt=""
        />
      </smart-link>
    </div>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  import eventPhoto from '../../scripts/eventPhoto';

  import SmartImage from '~/components/SmartImage.vue';
  import SmartLink from '~/components/SmartLink.vue';

  export default defineComponent({
    name: 'EventPhoto',
    components: {
      SmartImage,
      SmartLink,
    },
    props: {
      num: {
        type: Number,
      },
      src1: {
        type: String,
        require: true,
      },
      src2: {
        type: String,
        require: true,
      },
    },
    setup() {
      // let eventPhoto;
      // const newEventPhoto = [];
      //
      // for (let i = 0; i < eventPhoto.length; i = i + 2) {
      //   newEventPhoto.push(eventPhoto.photos[i], eventPhoto.photos[i + 1]);
      // }

      return {
        eventPhoto,
        // newEventPhoto,
      };
    },
  });
</script>

<style lang="scss" scoped>
  @import './css/settings';

  .slide {
    padding-top: map-get($units, xsmall) * 20;
    margin: auto;
    width: 100vw;
    //padding-bottom: 20px;
    //width: map-get($units, xsmall) * 334.14;
    //height: map-get($units, xsmall) * 329.03;
  }

  .smart-image {
    margin: auto auto map-get($units, xsmall) * 25;
    width: map-get($units, xsmall) * 334.14;
    height: map-get($units, xsmall) * 329.03;
  }

  .container {
    //padding: initial;
  }

  @include breakpoint(small) {
    .slide {
      padding-top: map-get($units, small) * 20;
      //width: map-get($units, small) * 559.94;
      //height: map-get($units, small) * 800;
    }

    .smart-image {
      margin-bottom: map-get($units, small) * 25;
      //width: map-get($units, small) * 559.94;
      //height: map-get($units, small) * 329.03;
      width: map-get($units, small) * 334.14;
      height: map-get($units, small) * 329.03;
    }
  }

  @include breakpoint(medium) {
    .event-photo-container {
      padding-right: map-get($units, medium) * 56.05;
    }

    .slide {
      padding-top: unset;
      width: unset;
      overflow: hidden;
    }

    .smart-image {
      padding-bottom: unset;
      //width: auto;
      //height: map-get($units, medium) * 329;
      //margin: 25px -121px 10px -120px;
      width: map-get($units, medium) * 203.13;
      height: map-get($units, medium) * 329.03;
    }
  }

  @include breakpoint(large) {
    .event-photo-container {
      padding-right: map-get($units, large) * 49.28;
    }

    .slide {
      //width: map-get($units, large) * 182.51;
      //height: map-get($units, large) * 329.03;
    }

    .smart-image {
      //padding-bottom: map-get($units, large) * 25;
      //width: auto;
      //height: map-get($units, large) * 329.03;
      //margin: 25px -121px 10px -120px;
      width: map-get($units, large) * 182.51;
      height: map-get($units, large) * 329.03;
    }

    //.container {
    //  padding: initial;
    //  height: 200px;
    //}
  }

  @include breakpoint(xlarge) {
    .event-photo-container {
      padding-right: map-get($units, xlarge) * 88.52;
    }

    .slide {
      //width: map-get($units, xlarge) * 253.77;
      //height: map-get($units, xlarge) * 329.03;
    }

    .smart-image {
      //padding-bottom: map-get($units, xlarge) * 25;
      //width: map-get($units, xlarge) * 253.77;
      //height: map-get($units, xlarge) * 329.03;
      //margin: 25px -77px 10px -96px;
      width: map-get($units, xlarge) * 253.79;
      height: map-get($units, xlarge) * 329.03;
    }
  }

  @include breakpoint(xxlarge) {
    .event-photo-container {
      padding-right: map-get($units, xxlarge) * 88.84;
    }

    .slide {
      position: center;
      //width: map-get($units, xxlarge) * 329.03;
      //height: map-get($units, xxlarge) * 329.03;
    }

    .smart-image {
      //padding-bottom: map-get($units, xxlarge) * 25;
      //width: map-get($units, xxlarge) * 329.03;
      //height: map-get($units, xxlarge) * 329.03;
      //margin: 25px -97px 10px -59px;
      width: map-get($units, xxlarge) * 329.03;
      height: map-get($units, xxlarge) * 329.03;
    }

    .container {
      padding: 0 40px;
    }
  }
</style>
