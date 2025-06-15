<script lang="ts">
import { defineComponent, nextTick } from "vue";
import gsap from "gsap";

export default defineComponent({
  name: "CitizenWrapper",
  props: {
    imgSrc: { type: String, required: true },
    imgAlt: { type: String, default: "" },
    name: { type: String, required: true },
    description: { type: String, required: true },
  },
  data() {
    return {
      observer: null as IntersectionObserver | null,
    };
  },
  mounted() {
    nextTick(() => {
      const el = this.$refs.cardRef as HTMLElement;
      if (!el) return;

      gsap.set(el, { opacity: 0, y: 50 });

      this.observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              gsap.killTweensOf(el);
              gsap.fromTo(
                el,
                { opacity: 0, y: 50 },
                { opacity: 1, y: 0, duration: 0.8, ease: "power2.out" }
              );
            } else {
              gsap.set(el, { opacity: 0, y: 50 });
            }
          });
        },
        { threshold: 0.3 }
      );

      this.observer.observe(el);
    });
  },
  beforeUnmount() {
    if (this.observer) {
      this.observer.disconnect();
    }
  },
});
</script>

<template>
  <div class="citizen-wrapper" ref="cardRef">
    <img :src="imgSrc" :alt="imgAlt" />
    <h4>{{ name }}</h4>
    <p>{{ description }}</p>
  </div>
</template>

<style scoped lang="scss">
.citizen-wrapper {
  display: flex;
  flex-direction: column;
  text-align: center;
  gap: 0.5rem;
  opacity: 0;

  img {
    filter: grayscale(100%);
  }

  h4 {
    font-weight: 400;
    font-size: 22px;
  }

  p {
    font-weight: 400;
  }
}

@media (max-width: 768px) {
  .citizen-wrapper {
    h4 {
      font-size: 14px;
    }

    p {
      font-size: 12px;
    }

    img {
      width: 100%;
    }
  }
}
</style>
