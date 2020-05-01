<template>
  <div class="card entity" :id="'plant-'+entity.id" :draggable="true" :data-entity="JSON.stringify(entity)">
    <a href="#" class="remove-entity" style="display:none">x</a>
    <div class="entity-name">
      {{ entity.name }}
      <br />
      {{ entity.no_of_item }}x
    </div>
    <div
      class="entity-image"
      :style="'background-image: url('+ entity.image +'); background-size:cover'"
    ></div>
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
  }
};
</script>