<template>
  <div id="content">
    <div class="row container" style="margin: 10px;flex: 1;">
      <div class="col card" style="justify-content: space-between; flex: 12">
        <div class="row grid-container">
          <div id="grid">
            <div class="row" v-for="i in rows" :key="i">
              <div
                class="cell"
                @drop.prevent="drop"
                @dragover.prevent
                v-for="j in columns"
                :key="j"
              ></div>
            </div>
          </div>
        </div>
        <div class="row" style="flex:1;margin: auto">
          <button class="btn btn-primary">
            Save
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    rows: {
      type: Number,
      default: 1
    },
    columns: {
      type: Number,
      default: 1
    }
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