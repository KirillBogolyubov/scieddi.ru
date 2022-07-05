<template>
  <div class="the-footer container">
    <div class="the-footer__content">
      <p class="the-footer__content-text">
        2021 (с) Институт Цифрового Развития Науки и Образования.
      </p>
      <p class="the-footer__content-text">Все права защищены.</p>
    </div>
    <a class="the-footer__button" href="mailto:admin@scieddi.ru">
      <div class="the-footer__button-icon">
        <img src="../assets/icons/envelop.svg" alt="envelop" />
      </div>
      <div class="the-footer__button-link">admin@scieddi.ru</div>
    </a>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    components: {},
    setup() {
      return {};
    },
  });
</script>

<style lang="scss" scoped>
  @import '../css/components/footer';

  @include footer(the-footer);
</style>
