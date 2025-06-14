<script lang="ts">
import gsap from "gsap";
import { defineComponent, nextTick, type PropType } from "vue";

interface Slides {
  src: string;
  alt: string;
}

export default defineComponent({
  name: "LogoSlideshow",
  props: {
    slides: {
      type: Array as PropType<Slides[]>,
      required: true,
    },
  },
  data() {
    return {
      currentIndex: 0,
      intervalId: 0,
      observer: null as IntersectionObserver | null,
    };
  },
  methods: {
    async animateSlideChange() {
      const logo = this.$refs.logoImage as HTMLElement;

      await gsap.to(logo, {
        y: 190,
        opacity: 0.1,
        duration: 0.2,
        ease: "power2.out",
      });

      this.currentIndex = (this.currentIndex + 1) % this.slides.length;
      await nextTick();

      const newLogo = this.$refs.logoImage as HTMLElement;

      gsap.set(newLogo, { y: -80, opacity: 0 });

      gsap.to(newLogo, {
        y: 0,
        opacity: 1,
        duration: 0.2,
        ease: "power2.out",
      });
    },
    startAutoSlide() {
      if (!this.intervalId) {
        this.intervalId = setInterval(this.animateSlideChange, 3000);
      }
    },
    stopAutoSlide() {
      clearInterval(this.intervalId);
      this.intervalId = 0;
    },
  },
  mounted() {
    const logoContainer = this.$refs.logoContainer as HTMLElement;

    this.observer = new IntersectionObserver(
      (entries) => {
        if (entries[0].isIntersecting) {
          this.startAutoSlide();
        } else {
          this.stopAutoSlide();
        }
      },
      { threshold: 0.3 }
    );

    this.observer.observe(logoContainer);
  },
  beforeUnmount() {
    this.stopAutoSlide();
    if (this.observer) {
      this.observer.disconnect();
    }
  },
});
</script>

<template>
  <div class="logo" ref="logoContainer">
    <img
      :src="slides[currentIndex].src"
      :alt="slides[currentIndex].alt"
      ref="logoImage"
    />
  </div>
</template>

<style lang="scss" scoped>
.logo {
  width: 180px;

  img {
    width: 100%;
    height: 170px;
    display: block;
  }
}
</style>
