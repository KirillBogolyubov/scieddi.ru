<template>
  <svg
    width="117"
    height="27"
    viewBox="0 0 117 27"
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
    <path
      d="M35.4355 20.9753H37.3764L46.1311 9.60473V20.9753H48.1985V6.20832H46.2577L37.524 17.6V6.20832H35.4355V20.9753Z"
      fill="#F3F3F3"
    />
    <path
      d="M65.2068 19.14V6.20832H63.1183V19.14H54.8909V6.20832H52.8025V20.9753H65.5232V24.3296H67.4851V19.14H65.2068Z"
      fill="#F3F3F3"
    />
    <path
      d="M76.0521 6.20832H70.293V20.9753H72.4026V16.503H76.0521C79.8915 16.503 82.2121 14.5622 82.2121 11.3557C82.2121 8.14913 79.8915 6.20832 76.0521 6.20832ZM75.9888 14.6677H72.4026V8.04365H75.9888C78.6891 8.04365 80.1025 9.2461 80.1025 11.3557C80.1025 13.4653 78.6891 14.6677 75.9888 14.6677Z"
      fill="#F3F3F3"
    />
    <path
      d="M95.7366 6.20832V12.5581H87.2561V6.20832H85.1465V20.9753H87.2561V14.3935H95.7366V20.9753H97.8462V6.20832H95.7366Z"
      fill="#F3F3F3"
    />
    <path
      d="M109.097 21.1441C113.59 21.1441 116.923 17.9376 116.923 13.5918C116.923 9.2461 113.59 6.03955 109.097 6.03955C104.561 6.03955 101.228 9.2672 101.228 13.5918C101.228 17.9165 104.561 21.1441 109.097 21.1441ZM109.097 19.2666C105.785 19.2666 103.338 16.8617 103.338 13.5918C103.338 10.322 105.785 7.91707 109.097 7.91707C112.367 7.91707 114.814 10.322 114.814 13.5918C114.814 16.8617 112.367 19.2666 109.097 19.2666Z"
      fill="#F3F3F3"
    />
  </svg>
</template>

<script lang="ts">
  import { defineComponent } from '@nuxtjs/composition-api';

  export default defineComponent({
    name: 'LogoOld',
  });
</script>

<style lang="scss" scoped>
  .scieddi-logo {
    animation: 1s appear;
    margin: auto;
  }

  @keyframes appear {
    0% {
      opacity: 0;
    }
  }
</style>
