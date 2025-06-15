<script lang="ts">
import { defineComponent } from "vue";
import ProjectWrapper from "./project-wrapper.vue";
import { worksList } from "../_data/works-list";

export default defineComponent({
  name: "Work",
  components: {
    ProjectWrapper,
  },
  data() {
    return {
      worksList,
    };
  },
});
</script>

<template>
  <div class="work">
    <div class="work__header">
      <h2>We want to help</h2>
      <p>
        homeless packs, volunteers, guardians, overstayers, shelters and other
        organisations
      </p>
    </div>

    <div class="work__workList">
      <ProjectWrapper
        v-for="(work, index) in worksList"
        :key="index"
        backgroundColor="#fff"
        :title="work.title"
        :href="work.href"
        width="100%"
        height="110px"
        slide-direction="bottom"
        text-color="#000"
        border-color="#000"
        font-size="sm"
        font-weight="600"
      />

      <a href="#" class="btn-link">
        apply for help
        <div class="btn-icon">
          <img
            src="../assets/images/btn-icons/6273a272fe3407579aa3d6c9_PngItem_344959.png"
            alt="arrow-right"
          />
        </div>
      </a>
    </div>
  </div>
</template>

<style lang="scss">
.work {
  background-color: #fcf944;
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

  &__workList {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;

    .btn-link {
      background-color: #ff97d0;
      max-width: 90%;
      text-decoration: none;
      text-align: center;
      padding: 14px 24px;
      border: 3.5px solid #000;
      color: #000;
      font-weight: 700;
      font-size: 22px;
      margin-top: 80px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 1rem;
      transition: background-color 0.3s ease;

      .btn-icon {
        display: flex;
        align-items: center;
        justify-content: center;

        img {
          width: 42px;
          height: auto;
          transform: rotate(180deg);
          transition: transform 0.3s ease, translate 0.3s ease;
        }
      }

      &:hover .btn-icon img {
        transform: rotate(180deg) translateX(-10px);
      }
    }
  }
}
</style>
