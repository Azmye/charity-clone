<script lang="ts">
import gsap from "gsap";
import { defineComponent, type PropType } from "vue";

export default defineComponent({
  name: "ProjectWrapper",
  props: {
    backgroundColor: {
      type: String as PropType<string>,
      default: "#000",
    },
    title: {
      type: String as PropType<string>,
      required: true,
    },
    paragraph: {
      type: String as PropType<string>,
      required: true,
    },
    href: {
      type: String as PropType<string>,
      required: true,
    },
  },
  mounted() {
    const wrapper = this.$refs.projectWrapper as HTMLElement;
    const inner = this.$refs.projectInnerWrapper as HTMLElement;

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            gsap.fromTo(
              wrapper,
              { opacity: 0, x: -100 },
              {
                opacity: 1,
                x: 0,
                duration: 2.5,
                ease: "power3.out",
              }
            );
          }
        });
      },
      { threshold: 0.3 }
    );

    observer.observe(wrapper);

    inner.addEventListener("mouseenter", () => {
      gsap.to(inner, {
        y: -20,
        x: 20,
        duration: 0.5,
        ease: "power2.out",
      });
    });

    inner.addEventListener("mouseleave", () => {
      gsap.to(inner, {
        y: 0,
        x: 0,
        duration: 0.5,
        ease: "power2.out",
      });
    });
  },
});
</script>

<template>
  <a
    class="project-wrapper"
    :href="href"
    :style="{ backgroundColor }"
    ref="projectWrapper"
  >
    <div class="project-inner-wrapper" ref="projectInnerWrapper">
      <h5>{{ title }}</h5>
      <p>{{ paragraph }}</p>
    </div>
  </a>
</template>

<style lang="scss" scoped>
.project-wrapper {
  display: block;
  text-decoration: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
  color: white;
}

.project-inner-wrapper {
  border: 3px solid #fff;
  padding: 3.2rem 3.2rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;

  h5 {
    font-size: 2.3rem;
  }

  p {
    font-size: 1.5rem;
  }
}
</style>
