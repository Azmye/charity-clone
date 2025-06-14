<script lang="ts">
import { defineComponent } from "vue";
import ProjectWrapper from "./project-wrapper.vue";

export default defineComponent({
  name: "OurProjects",
  components: {
    ProjectWrapper,
  },
});
</script>

<template>
  <div class="our-project">
    <div class="our-project__header">
      <h2>Our Projects</h2>
      <p>
        are very different in terms of priority, scale and complexity of
        implementation
      </p>
    </div>

    <div class="our-project__content">
      <ProjectWrapper
        backgroundColor="#000"
        title="Emergency Aid. WAR 2022."
        paragraph="providing food and medicine to the shelters and animals which lost their homes and families due to the war"
        href="https://example.com/project-details"
      />

      <ProjectWrapper
        backgroundColor="#31be32"
        title="Non-commercial feed line"
        paragraph="construction of industrial production base where food for shelters will be produced on a free basis "
        href="https://example.com/project-details"
      />

      <ProjectWrapper
        backgroundColor="#ff97d0"
        title="Education and Control"
        paragraph="lectures on communication, organisation and coordination of processes, control over the use of aid"
        href="https://example.com/project-details"
      />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.our-project {
  background-color: #3e88ff;
  display: flex;
  flex-direction: column;
  padding: 5rem 8rem;
  color: #fff;

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
    display: flex;
    flex-direction: column;
    gap: 3rem;
  }
}
</style>
