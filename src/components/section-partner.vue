<script lang="ts">
import { defineComponent, nextTick } from "vue";
import gsap from "gsap";
import { partnerList } from "../_data/partner-list";

export default defineComponent({
  name: "Partner",
  data() {
    return {
      partnerList,
    };
  },
  mounted() {
    nextTick(() => {
      const items = this.$refs.partnerRefs as HTMLElement[] | HTMLElement;
      if (!Array.isArray(items)) return;

      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            const el = entry.target as HTMLElement;

            if (entry.isIntersecting) {
              // Cancel any previous GSAP tweens on this element
              gsap.killTweensOf(el);

              gsap.fromTo(
                el,
                { opacity: 0, y: 100 },
                {
                  opacity: 1,
                  y: 0,
                  duration: 1,
                  ease: "power3.out",
                }
              );
            } else {
              // Optionally reset it so it's ready for next entrance
              gsap.set(el, { opacity: 0, y: 100 });
            }
          });
        },
        {
          threshold: 0.3,
        }
      );

      items.forEach((item) => {
        gsap.set(item, { opacity: 0, y: 100 }); // initial state
        observer.observe(item);
      });
    });
  },
});
</script>

<template>
  <div class="partner">
    <div class="partner__header">
      <h2>Our partners</h2>
      <p>are take care of our fund and help us with many questions</p>
    </div>

    <div class="partner__content">
      <div
        v-for="(item, index) in partnerList"
        :key="index"
        class="partner-wrapper"
        ref="partnerRefs"
      >
        <img :src="item.src" :alt="item.alt" />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.partner {
  display: flex;
  flex-direction: column;
  padding: 5rem 8rem;

  &__header {
    margin-bottom: 60px;

    h2 {
      font-size: 3rem;
    }

    p {
      font-size: 2rem;
      text-align: left;
    }
  }

  &__content {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 2rem;

    .partner-wrapper {
      display: flex;
      justify-content: center;

      img {
        width: 100%;
        object-fit: contain;
        filter: grayscale(100%);
      }
    }
  }
}

@media (max-width: 768px) {
  .partner {
    padding: 2rem;

    &__header {
      margin-bottom: 30px;
      h2 {
        font-size: 2rem;
      }

      p {
        font-size: 1rem;
      }
    }

    &__content {
      grid-template-columns: repeat(2, 1fr);
      gap: 1.5rem;
    }
  }
}
</style>
