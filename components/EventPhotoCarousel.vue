<template>
  <div class="event-photo-carousel">
    <div class="event-photo-carousel__progress">
      <counter-progress :options="carouselOptions" :max="photoList.length" />
    </div>
    <carousel-canvas
      ref="eventPhotoCarouselCanvas"
      v-model="carouselOptions"
      class="event-photo-carousel__canvas"
      :start-width-offset="740"
      :matrix-of-delta="[
        {
          width: 740,
          deltaOffset:
            photoList.length > 3
              ? 0 + (photoList.length % 2)
              : photoList.length - 1 || 1,
        },
      ]"
    >
      <event-photo
        v-for="(photo, index) in photoList1"
        :key="`photo-${index}`"
        :slot="`slot-${index}`"
        class="event-photo"
        :src1="photo[0]"
        :src2="photo[1]"
        :num="index"
      />
    </carousel-canvas>
    <div class="event-photo-carousel__buttons">
      <round-button
        mode="left"
        @click="$refs.eventPhotoCarouselCanvas.setPrevSlide()"
      />
      <round-button
        mode="right"
        @click="$refs.eventPhotoCarouselCanvas.setNextSlide()"
      />
    </div>
  </div>
</template>

<script lang="ts">
  import { defineComponent, PropType, ref } from '@nuxtjs/composition-api';

  import CarouselCanvas from '~/components/CarouselCanvas.vue';
  import RoundButton from '~/components/RoundButton.vue';
  import EventPhoto from '~/components/atoms/EventPhoto.vue';
  import CounterProgress from '~/components/CounterProgress.vue';
  import CarouselValue from '~/models/CarouselValue';

  export default defineComponent({
    name: 'EventPhotoCarousel',
    components: {
      CarouselCanvas,
      RoundButton,
      EventPhoto,
      CounterProgress,
    },
    props: {
      photoList: {
        type: Array as PropType<string[]>,
        default: [''],
        require: true,
      },
    },
    setup(props) {
      const carouselOptions = ref(new CarouselValue(0, 0));

      const photoList1: string[][] = ((eventPhotoList: string[]) => {
        const listOfPhotoPairs = [];

        for (let i = 0; i < eventPhotoList.length; i += 2) {
          listOfPhotoPairs.push([eventPhotoList[i], eventPhotoList[i + 1]]);
        }

        return listOfPhotoPairs;
      })(props.photoList);

      return {
        carouselOptions,
        CarouselValue,
        photoList1,
      };
    },
  });
</script>

<style lang="scss" scoped>
  @import './css/settings';
  @import './css/particles/container';

  //.carousel-canvas {
  //  overflow: visible;
  //  display: flex;
  //  position: relative;
  //}

  .event-photo-carousel {
    @extend %container;

    display: grid;
    grid-template-areas: 'event-photo-carousel-progress' 'event-photo-carousel-canvas' 'event-photo-carousel-buttons';
    margin-bottom: map-get($units, xsmall) * 80;

    &__progress {
      grid-area: event-photo-carousel-progress;
    }

    &__canvas {
      grid-area: event-photo-carousel-canvas;
    }

    &__buttons {
      grid-area: event-photo-carousel-buttons;
      align-items: center;
      display: grid;
      grid-template-columns:
        map-get($units, xsmall) * 53.95
        map-get($units, xsmall) * 53.95;
      grid-column-gap: map-get($units, xsmall) * 18.93;
      margin: auto;
      width: map-get($units, xsmall) * (53.95 * 2 + 18.93);
    }
  }

  @include breakpoint(small) {
    .event-photo-carousel {
      margin-bottom: map-get($units, small) * 80;

      &__buttons {
        grid-template-columns:
          map-get($units, small) * 53.95
          map-get($units, small) * 53.95;
        grid-column-gap: map-get($units, small) * 18.93;
        width: map-get($units, small) * (53.95 * 2 + 18.93);
      }
    }
  }

  @include breakpoint(small down) {
    .event-photo-carousel {
      padding: 0;
    }
  }

  @include breakpoint(medium) {
    .event-photo-carousel {
      margin-bottom: map-get($units, medium) * 80;
      grid-template-areas: 'event-photo-carousel-canvas event-photo-carousel-progress' 'event-photo-carousel-canvas event-photo-carousel-buttons';
      grid-template-columns: 1fr map-get($units, medium) * 250;

      &__progress {
        display: flex;
        align-items: flex-end;
        justify-content: center;
      }

      &__buttons {
        grid-template-columns:
          map-get($units, medium) * 53.95
          map-get($units, medium) * 53.95;
        grid-column-gap: map-get($units, medium) * 18.93;
        width: map-get($units, medium) * (53.95 * 2 + 18.93);
      }
    }
  }

  @include breakpoint(large) {
    .event-photo-carousel {
      //grid-template-areas: 'employee-carousel-canvas employee-carousel-progress' 'employee-carousel-canvas employee-carousel-buttons';
      //grid-template-columns: 1fr map-get($units, large) * 300;
      margin-bottom: map-get($units, large) * 80;
      grid-template-columns: 1fr map-get($units, large) * 250;

      &__progress {
        display: flex;
        align-items: flex-end;
        justify-content: center;
      }

      &__buttons {
        grid-template-columns:
          map-get($units, large) * 53.95
          map-get($units, large) * 53.95;
        grid-column-gap: map-get($units, large) * 18.93;
        width: map-get($units, large) * (53.95 * 2 + 18.93);
        padding-bottom: map-get($units, large) * 80;
      }
    }
  }

  @include breakpoint(xlarge) {
    .event-photo-carousel {
      margin: 0 map-get($units, xlarge) * 0 map-get($units, xlarge) * 80
        map-get($units, xlarge) * 0;
      grid-template-columns: 1fr map-get($units, xlarge) * 250;

      &__buttons {
        grid-template-columns:
          map-get($units, xlarge) * 53.95
          map-get($units, xlarge) * 53.95;
        grid-column-gap: map-get($units, xlarge) * 18.93;
        width: map-get($units, xlarge) * (53.95 * 2 + 18.93);
      }
    }
  }

  @include breakpoint(xxlarge) {
    .event-photo-carousel {
      margin: 0 map-get($units, xxlarge) * 0 map-get($units, xxlarge) * 80
        map-get($units, xxlarge) * 0;
      grid-template-columns: 1fr map-get($units, xxlarge) * 250;

      &__buttons {
        grid-template-columns:
          map-get($units, xxlarge) * 53.95
          map-get($units, xxlarge) * 53.95;
        grid-column-gap: map-get($units, xxlarge) * 18.93;
        width: map-get($units, xxlarge) * (53.95 * 2 + 18.93);
      }
    }
  }
</style>
