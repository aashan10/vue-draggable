<template>
  <div id="sidebar">
    <div class="row">
      <slot />
    </div>
    <div class="col">
      <div class="row">
        <h4>Plants</h4>
      </div>
      <div class="row plant-container" @drop.prevent="drop" @dragover.prevent>
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
            name: "Cauliflower",
            image: "/cauliflower.png"
          },
          {
            id: 2,
            name: "Lettuce",
            image: "/lettuce.png"
          },
          {
            id: 3,
            name: "Carrots",
            image: "/carrot.png"
          },
          {
            id: 4,
            name: "Strawberry",
            image: "/strawberry.png"
          },
          {
            id: 5,
            name: "Onion",
            image: "/onion.png"
          },
          {
            id: 6,
            name: "Garlic",
            image: "/garlic.png"
          }
        ];
      }
    }
  },
  components: {
    Plant
  },
  methods: {
    drop: e => {
      const target = e.target;
      const entityId = e.dataTransfer.getData("entity");
      const element = document.getElementById(entityId);
      target.appendChild(element);
    }
  }
};
</script>