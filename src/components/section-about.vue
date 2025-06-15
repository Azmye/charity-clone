<script lang="ts">
import gsap from "gsap";
import { defineComponent } from "vue";

export default defineComponent({
  name: "About",
  mounted() {
    const animatedElement = this.$refs.animatedElement as HTMLElement;

    gsap.set(animatedElement, {
      opacity: 0,
      y: 60,
    });

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            gsap.to(animatedElement, {
              opacity: 1,
              y: 0,
              duration: 0.8,
              ease: "power2.out",
            });
          } else {
            gsap.to(animatedElement, {
              opacity: 0,
              y: 80,
              duration: 0.6,
              ease: "power2.in",
            });
          }
        });
      },
      {
        threshold: 0.2,
        rootMargin: "0px 0px -50px 0px",
      }
    );

    observer.observe(animatedElement);
  },
});
</script>

<template>
  <div class="container" ref="container">
    <div class="wrapper">
      <h1>We are</h1>
      <p>
        team of like-minded people, socially active companies, media
        personalities, volunteers who help low-income shelters and foster carers
        to support homeless animals.
      </p>
    </div>
    <div class="wrapper">
      <h1>Our primary goal</h1>
      <p>
        is to provide animals with the most necessary things - food, medicine,
        and urgent needs for the livelihood of shelters. We believe in our power
        and the power of conscious citizens who care about the environment and
        their health, who understand the importance of helping each other,
        especially our little friends. Growth begins with your care for your
        loved ones. Animals are one of the closest creatures to humans who
        remain with us throughout our lives. We all know the healing power of
        warmth, grace, and big loving eyes.

        <span class="block--quotes">
          "Animals need to have friends. Just like humans."
          <br />
          - James Herriot, All Creatures Great and Small
        </span>

        Who else if not we should support our younger brothers, especially in
        difficult times? Let's be friends!
      </p>
    </div>

    <div class="iframe-container">
      <div class="iframe-animated" ref="animatedElement">
        <div class="iframe-wrapper">
          <iframe
            src="https://www.youtube.com/embed/5Wk1rp99B7o?si=Gezsl2ZHpzVDCdaK"
            title="YouTube video player"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
            referrerpolicy="strict-origin-when-cross-origin"
            allowfullscreen
          ></iframe>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  padding: 5rem 8rem;
  gap: 2rem;
  margin-bottom: 20px;
}

.wrapper {
  h1 {
    font-size: 4vw;
  }
  p {
    font-size: 2.5vw;
    text-align: left;
  }
}

.block--quotes {
  border-left: 4px solid #ff97d0;
  padding: 1rem 0rem 1rem 1rem;
  display: block;
  margin: 2rem 0rem 2rem 4rem;
  font-style: italic;
}

.iframe-container {
  width: 100%;
  padding-bottom: 56.25%;
  position: relative;
}

.iframe-animated {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.iframe-wrapper {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;

  iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border: 4px solid #000;
  }
}

@media (max-width: 768px) {
  .container {
    display: flex;
    flex-direction: column;
    padding: 2rem;
  }

  .wrapper {
    h1 {
      font-size: 1.8rem;
    }
    p {
      font-size: 0.9rem;
    }
  }

  .block--quotes {
    border-left: 4px solid #ff97d0;
    padding: 1rem 0rem 1rem 1rem;
    display: block;
    margin: 1rem 0rem 1rem 1rem;
    font-style: italic;
  }
}
</style>
