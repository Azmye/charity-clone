<script lang="ts">
import gsap from "gsap";
import { defineComponent, type PropType } from "vue";

// Define the shape of each social icon
interface SocialIcons {
  href: string;
  src: string;
  alt: string;
}

export default defineComponent({
  name: "SocialLinks",
  props: {
    // Accepts an array of social icons as props
    icons: Array as PropType<SocialIcons[]>,
  },
  mounted() {
    // Get the DOM elements using ref
    const socialLinks = this.$refs.socialLinks as HTMLElement[] | HTMLElement;

    // Normalize to an array in case only one element is returned
    const links = Array.isArray(socialLinks) ? socialLinks : [socialLinks];

    // Loop through each icon element
    links.forEach((el) => {
      // Animate on mouse enter (scale down)
      el.addEventListener("mouseenter", () => {
        gsap.to(el, { scale: 0.75, duration: 0.2 });
      });

      // Animate on mouse leave (scale back to normal)
      el.addEventListener("mouseleave", () => {
        gsap.to(el, { scale: 1, duration: 0.2 });
      });
    });
  },
});
</script>

<template>
  <div class="social-links">
    <a
      v-for="(icon, index) in icons"
      :key="index"
      :href="icon.href"
      class="social-icon"
      ref="socialLinks"
    >
      <img :src="icon.src" :alt="icon.alt" />
    </a>
  </div>
</template>

<style lang="scss">
.social-links {
  display: flex;
  justify-content: center;
  gap: 1rem;

  .social-icon {
    width: 48px;
    cursor: pointer;

    img {
      width: 100%;
      height: auto;
      display: block;
    }
  }
}

@media (max-width: 768px) {
  .social-links {
    .social-icon {
      width: 32px;
    }
  }
}
</style>
