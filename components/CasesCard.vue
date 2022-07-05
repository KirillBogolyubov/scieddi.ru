<template>
  <div class="cases-card">
    <div class="cases-card__head">
      <img :src="card.icon_url" alt="icon" />
      <div class="cases-card__head-count count-hover">{{ card.count }}</div>
    </div>
    <div class="cases-card__text">{{ card.name }}</div>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    name: 'CasesCard',
    components: {},
    props: {
      card: {
        type: Object,
        require: true,
      },
    },
  });
</script>

<style lang="scss" scoped>
  @import '../css/components/casesCard';

  @include casesCard(cases-card);
</style>
