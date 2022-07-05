<template>
  <header class="the-header">
    <div class="the-header__wrap container">
      <a href="/" class="the-header__link">
        <Logo />
      </a>
    </div>
  </header>
</template>

<script>
  import { defineComponent } from '@nuxtjs/composition-api';

  import Logo from '../components/Logo';

  export default defineComponent({
    name: 'HeadingH2',
    components: {
      Logo,
    },
    props: {
      heading: {
        type: String,
        require: true,
      },
      description: String,
    },
    setup() {
      return {};
    },
  });
</script>

<style lang="scss" scoped>
  @import '../css/components/header';

  @include header(the-header);
</style>
