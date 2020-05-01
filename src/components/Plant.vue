<template>
  <div
    class="card entity"
    :id="'plant-'+entity.id"
    :draggable="true"
    @dragstart="dragStart"
    @dragover.stop
  >
    <div class="entity-name">{{ entity.name }}</div>
    <img :src="entity.image" alt class="entity-image" />
  </div>
</template>

<script>
export default {
  props: {
    entity: {
      type: Object,
      default: () => {
        return {
          id: Math.random(),
          name: "Entity name",
          image: "https://placeholdd.it/50x50"
        };
      }
    }
  },
  methods: {
    dragStart: e => {
      const target = e.target;
      e.dataTransfer.setData("entity", target.id);
    }
  }
};
</script>