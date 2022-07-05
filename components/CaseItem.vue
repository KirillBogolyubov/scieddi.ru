<template>
  <div class="case-item">
    <div class="case-item__head">
      <img class="case-item__icon" :src="card.icon_url" alt="icon" />
    </div>
    <div class="case-item__text"><slot /></div>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    name: 'CaseItem',
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
  @import '../css/components/casesItem';

  @include casesItem(case-item);
</style>
