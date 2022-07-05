<template>
  <div class="card">
    <p class="card__text">{{ goal }}</p>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    name: 'Card',
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
  @import '../css/components/card';

  @include card(card);
</style>
