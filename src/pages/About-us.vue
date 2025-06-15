<script setup lang="ts">
import SectionAbout from "../components/section-about.vue";
import SectionCitizens from "../components/section-citizens.vue";
import SectionContact from "../components/section-contact.vue";
import SectionHero from "../components/section-hero.vue";
import SectionPartner from "../components/section-partner.vue";
import SectionProject from "../components/section-project.vue";
import SectionTeam from "../components/section-team.vue";
import SectionWork from "../components/section-work.vue";
</script>

<template>
  <div class="btn-donate">
    <a href="#">donate</a>
  </div>

  <SectionHero />

  <SectionAbout />

  <SectionProject />

  <SectionWork />

  <SectionTeam />

  <SectionCitizens />

  <SectionPartner />

  <SectionContact />

  <div class="copyright">
    <img src="../assets/vue.svg" alt="" />
    <a target="_blank" href="https://vuejs.org/">Made in vue</a>
  </div>
</template>

<style lang="scss">
.btn-donate {
  background-color: #fff;
  position: fixed;
  z-index: 1000;
  top: 20px;
  right: 20px;
  display: inline-flex;

  a {
    display: inline-block;
    text-decoration: none;
    border: 3px solid #000;
    padding: 3px 8px;
    font-weight: 400;
    color: #000;
    background-color: transparent;
    transition: transform 0.3s ease;

    &:hover {
      transform: translate(8px, -8px);
    }
  }
}

.copyright {
  position: fixed;
  bottom: 8px;
  right: 8px;
  background-color: #fff;
  border: 1px solid #000;
  border-radius: 2px;
  padding: 3px;
  display: flex;
  align-items: center;
  gap: 2px;

  img {
    width: 16px;
  }

  a {
    text-decoration: none;
    color: #000;
    font-weight: 600;
  }
}
</style>
