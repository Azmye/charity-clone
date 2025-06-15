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

    // Create an IntersectionObserver to trigger animations when the hero section enters the viewport
    const observer = new IntersectionObserver(
      (entries) => {
        if (entries[0].isIntersecting) {
          // Animate logo sliding in from top with fade
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

          // Animate title sliding in from the right with fade
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

          // Animate subtitle and social links sliding in from bottom with fade
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
        }
      },
      { threshold: 0.3 } // Trigger when 30% of the hero section is visible
    );

    // Start observing the hero section
    observer.observe(section);
  },
});
</script>

<template>
  <section class="hero" ref="section">
    <div class="hero__container" ref="container">
      <div class="hero__header">
        <div class="logo-slide-show" ref="logoSlideshow">
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

  @media (max-width: 768px) {
    .hero {
      padding: 2rem 1rem;
    }

    .hero__container {
      width: 100%;
      max-width: 100%;
    }

    .hero__header {
      flex-direction: row;
      gap: 1.5rem;
    }

    .hero__title {
      font-size: 1.2rem;
      text-align: left;
    }

    .hero__subtitle {
      font-size: 1rem;
    }
  }
}
</style>
