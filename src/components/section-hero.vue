<script lang="ts">
import { defineComponent } from "vue";
import { gsap } from "gsap";
import { socialIcons } from "../_data/social-icons";
import { heroLogos } from "../_data/hero-logos";
import LogoSlideshow from "./logo-slideshow.vue";
import SocialLinks from "./social-links.vue";

export default defineComponent({
  name: "Hero",
  components: {
    LogoSlideshow,
    SocialLinks,
  },
  data() {
    return {
      icons: socialIcons,
      slides: heroLogos,
    };
  },
  mounted() {
    const section = this.$refs.section as HTMLElement;
    const heroTitle = this.$refs.heroTitle as HTMLElement;
    const heroLogo = this.$refs.logoSlideshow as HTMLElement;
    const content = this.$refs.content as HTMLElement;

    const observer = new IntersectionObserver(
      (entries, observer) => {
        if (entries[0].isIntersecting) {
          gsap.fromTo(
            heroLogo,
            { opacity: 0, y: -60 },
            {
              opacity: 1,
              y: 0,
              duration: 1.3,
              ease: "power3.out",
            }
          );
          gsap.fromTo(
            heroTitle,
            { opacity: 0, x: 80 },
            {
              opacity: 1,
              x: 0,
              duration: 1.3,
              ease: "power3.out",
              stagger: 0.2,
            }
          );
          gsap.fromTo(
            content,
            { opacity: 0, y: 60 },
            {
              opacity: 1,
              y: 0,
              duration: 1.3,
              ease: "power3.out",
              stagger: 0.2,
            }
          );
          observer.disconnect();
        }
      },
      { threshold: 0.3 }
    );

    observer.observe(section);
  },
});
</script>

<template>
  <section class="hero" ref="section">
    <div class="hero__container" ref="container">
      <div class="hero__header">
        <div ref="logoSlideshow">
          <LogoSlideshow :slides="slides" />
        </div>
        <h1 ref="heroTitle" class="hero__title">
          Innovative<br />Solutions<br />for Animals
        </h1>
      </div>

      <div class="hero__content" ref="content">
        <div class="hero__subtitle">Charity Organization</div>
        <SocialLinks :icons="icons" />
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.hero {
  height: 100vh;
  background-color: #fcf944;
  display: flex;
  align-items: center;
  justify-content: center;

  &__container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    width: 80%;
    max-width: 800px;
  }

  &__header {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 2rem;
    flex-wrap: wrap;
    margin-bottom: 10px;
  }

  &__content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 0.8rem;
  }

  &__title {
    font-size: 4vw;
    line-height: 1.2;
    font-weight: bold;
  }

  &__subtitle {
    font-size: 1.85rem;
  }
}
</style>
