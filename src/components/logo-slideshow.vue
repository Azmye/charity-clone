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
      currentIndex: 0, // Index of the currently displayed slide
      intervalId: 0, // ID for the auto-slide interval
      observer: null as IntersectionObserver | null, // To watch when component is visible
    };
  },
  methods: {
    // Animate current slide out and next slide in
    async animateSlideChange() {
      const logo = this.$refs.logoImage as HTMLElement;

      // Animate current logo sliding down and fading out
      await gsap.to(logo, {
        y: 190,
        opacity: 0.1,
        duration: 0.2,
        ease: "power2.out",
      });

      // Move to next index and wait for DOM update
      this.currentIndex = (this.currentIndex + 1) % this.slides.length;
      await nextTick();

      const newLogo = this.$refs.logoImage as HTMLElement;

      // Set initial state for the new logo (above and transparent)
      gsap.set(newLogo, { y: -80, opacity: 0 });

      // Animate it sliding into view
      gsap.to(newLogo, {
        y: 0,
        opacity: 1,
        duration: 0.2,
        ease: "power2.out",
      });
    },

    // Start auto slide with setInterval
    startAutoSlide() {
      if (!this.intervalId) {
        this.intervalId = setInterval(this.animateSlideChange, 3000);
      }
    },

    // Stop auto slide and clear interval
    stopAutoSlide() {
      clearInterval(this.intervalId);
      this.intervalId = 0;
    },
  },

  mounted() {
    const logoContainer = this.$refs.logoContainer as HTMLElement;

    // Use IntersectionObserver to start/stop auto sliding only when visible
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
    // Clean up interval and observer when component is destroyed
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

@media (max-width: 768px) {
  .logo {
    width: 80px;

    img {
      width: 100%;
      height: 80px;
      display: block;
    }
  }
}
</style>
