<script lang="ts">
import { defineComponent } from "vue";
import { socialIcons } from "../_data/social-icons";
import SocialLinks from "./social-links.vue";

export default defineComponent({
  name: "contact",
  components: {
    SocialLinks,
  },
  data() {
    return {
      socialIcons,
    };
  },
});
</script>

<template>
  <div class="contact">
    <div class="contact__header">
      <h1>Contact us</h1>
      <p>Kyiv, Ukraine</p>
      <a href="">mail@isa.co.ua</a>

      <div class="social-links-wrapper">
        <SocialLinks :icons="socialIcons" />
      </div>
    </div>

    <div class="contact__content">
      <div class="content-image-wrapper">
        <img
          src="../assets/images/62647f9fbe07235ba9b28d67_star-white-with-animals.svg"
          alt="star-white-animals"
        />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.contact {
  background-color: #31be32;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 8rem;
  &__header {
    display: flex;
    flex-direction: column;
    align-items: left;
    width: 50%;

    h1 {
      font-size: 3.3rem;
    }
    p,
    a {
      font-size: 2.2rem;
      text-align: left;
      color: #000;
      text-decoration: none;
    }

    .social-links-wrapper {
      margin-top: 32px;
      display: flex;
      justify-content: left;
    }
  }
  &__content {
    width: 50%;
    img {
      width: 100%;
      object-fit: contain;
    }
  }
}

@media (max-width: 768px) {
  .contact {
    flex-direction: column;
    padding: 2rem;

    &__header {
      width: 100%;

      h1 {
        font-size: 2rem;
      }

      p,
      a {
        font-size: 0.9rem;
      }
    }

    .social-links-wrapper {
      margin-left: 10px;
    }

    &__content {
      width: 100%;
      margin-top: 3rem;

      .content-image-wrapper {
        width: 100%;
      }
    }
  }
}
</style>
