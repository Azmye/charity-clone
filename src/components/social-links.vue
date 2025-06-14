<script lang="ts">
import gsap from "gsap";
import { defineComponent, type PropType } from "vue";

interface SocialIcons {
  href: string;
  src: string;
  alt: string;
}

export default defineComponent({
  name: "SocialLinks",
  props: {
    icons: Array as PropType<SocialIcons[]>,
  },
  mounted() {
    const socialLinks = this.$refs.socialLinks as HTMLElement[] | HTMLElement;
    const links = Array.isArray(socialLinks) ? socialLinks : [socialLinks];

    links.forEach((el) => {
      el.addEventListener("mouseenter", () => {
        gsap.to(el, { scale: 0.75, duration: 0.2 });
      });
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
</style>
