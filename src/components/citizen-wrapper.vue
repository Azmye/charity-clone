<!-- components/CitizenCard.vue -->
<script lang="ts">
import { defineComponent, onMounted, ref } from "vue";
import gsap from "gsap";

export default defineComponent({
  name: "CitizenWrapper",
  props: {
    imgSrc: { type: String, required: true },
    imgAlt: { type: String, default: "" },
    name: { type: String, required: true },
    description: { type: String, required: true },
  },
  setup() {
    const cardRef = ref<HTMLElement | null>(null);

    onMounted(() => {
      const el = cardRef.value;
      if (!el) return;

      gsap.set(el, { opacity: 0, y: 50 });

      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              gsap.to(el, {
                opacity: 1,
                y: 0,
                duration: 0.8,
                ease: "power2.out",
              });
            } else {
              gsap.set(el, { opacity: 0, y: 50 });
            }
          });
        },
        { threshold: 0.3 }
      );

      observer.observe(el);
    });

    return {
      cardRef,
    };
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

  h4 {
    font-weight: 400;
    font-size: 22px;
  }

  p {
    font-weight: 400;
  }
}
</style>
