<script lang="ts">
import { defineComponent } from "vue";
import gsap from "gsap";

export default defineComponent({
  name: "TeamWrapper",
  props: {
    imgSrc: { type: String, required: true },
    imgAlt: { type: String, default: "" },
    name: { type: String, required: true },
    jobTitle: { type: String, required: true },
  },
  mounted() {
    const el = this.$refs.cardRef as HTMLElement;
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
  },
});
</script>

<template>
  <div class="team-wrapper" ref="cardRef">
    <div class="inner-wrapper">
      <img :src="imgSrc" :alt="imgAlt" />
      <h4>{{ name }}</h4>
      <p>{{ jobTitle }}</p>
    </div>
  </div>
</template>

<style scoped lang="scss">
.team-wrapper {
  display: flex;
  flex-direction: column;
  background-color: #e9e63f;
  height: 100%;

  .inner-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    background-color: transparent;
    border: 3.5px solid #000;
    padding: 32px 16px;
    transition: transform 0.3s ease;
    height: 100%;

    &:hover {
      transform: scale(0.9);
    }

    img {
      filter: grayscale(100%);
      width: 80%;
      margin-bottom: 1rem;
      transition: filter 0.3s ease;
    }

    h4 {
      margin-bottom: 0.3rem;
      font-weight: 400;
      font-size: 18px;
    }

    p {
      margin-bottom: 20px;
    }
  }
}

@media (max-width: 768px) {
  .team-wrapper {
    display: flex;
    flex-direction: column;
    background-color: #e9e63f;
    height: 95%;

    .inner-wrapper {
      display: flex;
      flex-direction: column;
      justify-content: start;
      // align-items: center;
      text-align: center;
      background-color: transparent;
      border: 3.5px solid #000;
      padding: 12px;
      transition: transform 0.3s ease;
      height: 100%;
      margin-bottom: auto;

      &:hover {
        transform: scale(0.9);
      }

      img {
        filter: grayscale(100%);
        width: 100%;
        transition: filter 0.3s ease;
      }

      h4 {
        margin-bottom: 0.3rem;
        font-weight: 500;
        font-size: 16px;
      }
    }
  }
}
</style>
