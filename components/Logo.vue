<template>
  <svg
    viewBox="0 -1 26 28"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
    class="scieddi-logo"
  >
    <path
      d="M24.5818 10.2464L24.5818 16.5138L2.7581 6.26732L2.75809 -8.9787e-05L24.5818 10.2464Z"
      fill="#F3F3F3"
    />
    <path
      fill-rule="evenodd"
      clip-rule="evenodd"
      d="M2.69849 26.8072L18.0127 19.617L18.0127 13.3496L2.69849 20.5398V26.8072Z"
      fill="white"
      fill-opacity="0.5"
    />
  </svg>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    name: 'Logo',
  });
</script>

<style lang="scss" scoped>
  .scieddi-logo {
    width: 100%;
  }
</style>
