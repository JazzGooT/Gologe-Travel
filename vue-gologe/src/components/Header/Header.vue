<template>
  <!-- Header wrapper Start -->
  <div class="header_wrapper animation" :class="{ animate: animationStore.headerIsAnimated }">
    <!-- Header Content Start -->
    <div class="header_content">
      <!-- Use Navigation UI Component -->
      <CustomNavigation
        :class="
          route.name !== 'Landing' ? 'text-custom-darkgreen' : 'text-default'
        "
      />
      <!-- Use Logo UI Component -->

      <!-- Use Logo UI Component -->
      <CustomLogo class="sm:hidden absolute left-1/2 -translate-x-1/2"/>

      <!-- Header Auth wrapper Start -->
      <div class="header-auth-wrapper">

        <!-- Use component if User not Login -->
        <HeaderLoggedOff/>
        <!-- Use component if User Is LoggedIn -->
        <HeaderLoggenIn/>
        <!-- Use Localization Component -->
        <Localization />
      </div>
      <!-- Header Auth wrapper End -->
    </div>
    <!-- Header Content End -->
  </div>
  <!-- Header wrapper End -->
</template>

<script setup lang="ts">
import HeaderLoggedOff from './HeaderLoggedOff.vue';
import HeaderLoggenIn from './HeaderLoggenIn.vue'
import Localization from "./Localization.vue";
import { useRoute } from "vue-router";
import { onMounted } from 'vue';
import { useAnimationStore } from '@/stores/animatiomStore';

const animationStore = useAnimationStore(),
  route = useRoute();

onMounted(() => {
  animationStore.startAnimation("headerIsAnimated", true, 100);
});
</script>

<style lang="scss" scoped>
.header_wrapper {
  @apply max-w-large-width w-full h-20 mx-auto px-[104px];

  @screen md {
    @apply px-12;
  }

  @screen sm {
    @apply px-12 h-[60px];
  }
  .header_content {
    @apply w-full h-full flex  items-center justify-between relative;

    .header-auth-wrapper {
      @apply max-w-[400px] w-full h-full flex items-center justify-end gap-4;
    }
  }
}

.animation {
  opacity: 0;
  transform: translateY(-30px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.animation.animate {
  opacity: 1;
  transform: translateY(0);
}
</style>
