<script lang="ts">
import { defineComponent } from "vue";
import TeamWrapper from "./team-wrapper.vue";
import { teamList } from "../_data/team-list";

export default defineComponent({
  name: "Team",
  data() {
    return {
      teamList,
    };
  },
  components: {
    TeamWrapper,
  },
});
</script>

<template>
  <div class="teams">
    <div class="teams__header">
      <h2>Our team</h2>
      <p>
        consists of completely different people who are united by a common
        desire - to help
      </p>
    </div>

    <div class="teams__content">
      <TeamWrapper
        v-for="(team, index) in teamList"
        :key="index"
        :imgSrc="team.src"
        :imgAlt="team.alt"
        :name="team.fullname"
        :jobTitle="team.position"
      />
    </div>
  </div>
</template>

<style lang="scss" scoped>
.teams {
  background-color: #fff;
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
    grid-template-columns: repeat(4, 1fr); // Default: 4 columns
    gap: 2rem;
  }
}

@media (max-width: 1024px) {
  .teams {
    padding: 4rem;

    &__header {
      h2 {
        font-size: 2.4rem;
      }

      p {
        font-size: 1.6rem;
      }
    }

    &__content {
      grid-template-columns: repeat(3, 1fr);
    }
  }
}

@media (max-width: 768px) {
  .teams {
    padding: 2rem;

    &__header {
      h2 {
        font-size: 2rem;
      }

      p {
        font-size: 1rem;
      }
    }

    &__content {
      grid-template-columns: repeat(2, 1fr);
    }
  }
}
</style>
