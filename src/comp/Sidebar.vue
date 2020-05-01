<template>
  <div class="sidebar" @drop.prevent="drop" @dragover.prevent>
    <slot />
    <h3 style="padding: 10px; color:white; font-weight: 600;">Entities</h3>
    <div class="row" style="flex-wrap: wrap; flex: none;">
      <Entity
        :draggable="true"
        v-for="entity of entities"
        :key="entity.id.toString()"
        :id="entity.id.toString()"
        class="max-width-100 max-height-100"
      >
        <b class="entity-name">{{entity.title}}</b>
        <div class="entity-thumbnail">
          <img :src="entity.image" />
        </div>
      </Entity>
    </div>
  </div>
</template>


<script>
import Entity from "./Entity";

export default {
  props: {
    entities: {
      type: Array,
      default: new Array()
    }
  },
  components: {
    Entity
  },
  methods: {
    drop: e => {
      const target = e.target;
      const entityId = e.dataTransfer.getData("entity");
      const element = document.getElementById(entityId);
      target.appendChild(element);
      element.classList.add("auto-height");
    }
  }
};
</script>