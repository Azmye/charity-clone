<script lang="ts">
import { defineComponent } from "vue";
import CitizenWrapper from "./citizen-wrapper.vue";
import { citizenList } from "../_data/citizen-list";

export default defineComponent({
  name: "Citizens",
  data() {
    return {
      citizenList,
    };
  },
  components: {
    CitizenWrapper,
  },
});
</script>

<template>
  <div class="citizens">
    <div class="citizens__header">
      <h2>Socially active citizens</h2>
      <p>support us</p>
    </div>

    <div class="citizens__content">
      <CitizenWrapper
        v-for="(item, index) in citizenList"
        :key="index"
        :name="item.fullname"
        :description="item.position"
        :img-src="item.src"
        :img-alt="item.alt"
      />
    </div>
  </div>
</template>

<style lang="scss">
.citizens {
  background-color: #ff97d0;
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
  }
}

@media (max-width: 768px) {
  .citizens {
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
    }
  }
}
</style>
