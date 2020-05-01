<template>
  <div id="sidebar">
    <div class="row">
      <slot />
    </div>
    <div class="col">
      <div class="row">
        <h4>Plants</h4>
      </div>
      <div class="row plant-container">
        <Plant v-for="plant in entities" :entity="plant" :key="plant.id" />
      </div>
    </div>
  </div>
</template>

<script>
import Plant from "./Plant";

export default {
  props: {
    entities: {
      type: Array,
      default: () => {
        return [
          {
            id: 1,
            no_of_item: 2,
            name: "Cauliflower",
            image: "/cauliflower.png"
          },
          {
            id: 2,
            no_of_item: 2,
            name: "Lettuce",
            image: "/lettuce.png"
          },
          {
            id: 3,
            no_of_item: 5,
            name: "Carrots",
            image: "/carrot.png"
          },
          {
            id: 4,
            name: "Strawberry",
            no_of_item: 10,
            image: "/strawberry.png"
          },
          {
            id: 5,
            name: "Onion",
            no_of_item: 12,
            image: "/onion.png"
          },
          {
            id: 6,
            name: "Garlic",
            no_of_item: 15,
            image: "/garlic.png"
          }
        ];
      }
    }
  },
  components: {
    Plant
  },
  methods: {}
};
</script>