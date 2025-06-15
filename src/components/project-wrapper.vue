<script lang="ts">
import { defineComponent, type PropType } from "vue";
import gsap from "gsap";

export default defineComponent({
  name: "ProjectWrapper",
  props: {
    fontWeight: {
      type: String as PropType<
        | "normal"
        | "bold"
        | "lighter"
        | "bolder"
        | "100"
        | "200"
        | "300"
        | "400"
        | "500"
        | "600"
        | "700"
        | "800"
        | "900"
        | string
      >,
      default: "bold",
    },

    backgroundColor: {
      type: String as PropType<string>,
      default: "#000",
    },
    textColor: {
      type: String as PropType<string>,
      default: "#ffffff",
    },
    fontSize: {
      type: String as PropType<"sm" | "md" | "lg" | "xl" | "2xl">,
      default: "md",
    },
    title: {
      type: String,
      required: true,
    },
    paragraph: {
      type: String,
      default: "",
    },
    href: {
      type: String,
      required: true,
    },
    slideDirection: {
      type: String as PropType<"left" | "right" | "top" | "bottom" | "fade">,
      default: "left",
    },
    width: {
      type: String,
      default: "100%",
    },
    height: {
      type: String,
      default: "auto",
    },
    borderColor: {
      type: String,
      default: "#fff",
    },
  },
  computed: {
    computedFontSize(): string {
      switch (this.fontSize) {
        case "sm":
          return "1rem";
        case "md":
          return "1.5rem";
        case "lg":
          return "2rem";
        case "xl":
          return "2.5rem";
        case "2xl":
          return "3rem";
        default:
          return "1.5rem";
      }
    },
  },
  mounted() {
    const wrapper = this.$refs.projectWrapper as HTMLElement;
    const inner = this.$refs.projectInnerWrapper as HTMLElement;

    const getAnimationOffset = () => {
      switch (this.slideDirection) {
        case "right":
          return { x: 100, y: 0 };
        case "top":
          return { x: 0, y: -100 };
        case "bottom":
          return { x: 0, y: 100 };
        case "fade":
          return { x: 0, y: 0 };
        case "left":
        default:
          return { x: -100, y: 0 };
      }
    };

    const { x, y } = getAnimationOffset();
    gsap.set(wrapper, { opacity: 0, x, y });

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            gsap.fromTo(
              wrapper,
              { opacity: 0, x, y },
              { opacity: 1, x: 0, y: 0, duration: 1.5, ease: "power3.out" }
            );
          } else {
            gsap.set(wrapper, { opacity: 0, x, y });
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
    :style="{
      backgroundColor,
      width,
      height,
      color: textColor,
    }"
    ref="projectWrapper"
  >
    <div
      class="project-inner-wrapper"
      :class="{ 'center-content': !paragraph }"
      :style="{ borderColor }"
      ref="projectInnerWrapper"
    >
      <h5 :style="{ fontSize: computedFontSize, fontWeight }">{{ title }}</h5>
      <p v-if="paragraph" :style="{ fontSize: computedFontSize }">
        {{ paragraph }}
      </p>
    </div>
  </a>
</template>

<style lang="scss" scoped>
.project-wrapper {
  display: block;
  text-decoration: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.project-inner-wrapper {
  border-width: 3px;
  border-style: solid;
  padding: 3.2rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;

  h5,
  p {
    margin: 0;
  }
}

.center-content {
  justify-content: center;
  align-items: center;
  text-align: center;
  height: 100%;
  display: flex;
  flex-direction: column;
}

@media (max-width: 768px) {
  .project-wrapper {
    width: 100% !important; // override if prop width is too wide
    height: auto !important;
  }

  .project-inner-wrapper {
    padding: 2rem;
    gap: 0.75rem;
  }

  .project-inner-wrapper h5 {
    font-size: 1.5rem !important;
  }

  .project-inner-wrapper p {
    font-size: 1rem !important;
  }
}
</style>
