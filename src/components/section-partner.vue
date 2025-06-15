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
    // Wait for the DOM to be fully updated/rendered before querying refs
    nextTick(() => {
      const items = this.$refs.partnerRefs as HTMLElement[] | HTMLElement;
      if (!Array.isArray(items)) return; // Guard clause if only one element is returned

      // Set up an IntersectionObserver to animate each item when it enters the viewport
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            const el = entry.target as HTMLElement;

            if (entry.isIntersecting) {
              // Stop any ongoing animation on the element to avoid conflicts
              gsap.killTweensOf(el);

              // Animate element in: fade in and move up
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
              // Reset element when it leaves the viewport
              gsap.set(el, { opacity: 0, y: 100 });
            }
          });
        },
        {
          threshold: 0.3, // Animation triggers when 30% of the element is visible
        }
      );

      // Set initial state and observe each partner item
      items.forEach((item) => {
        gsap.set(item, { opacity: 0, y: 100 });
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
