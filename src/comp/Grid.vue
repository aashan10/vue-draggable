<template>
  <!-- <div class="card" style="flex-direction: column">
    
  </div>-->
  <div class="card" style="flex-direction: column; justify-content: space-between; margin: 0 auto; flex: none;">
    <div style=" background-color: #774508; border-radius: 10px; width: fit-content;">
      <div class="row auto-height" style="width: fit-content;" v-for="i in rows" v-bind:key="i">
        <div
          class="col cell"
          v-for="j in columns"
          v-bind:key="'cell-'+i+'-'+j"
          v-bind:id="'cell-'+i+'-'+j"
          @drop.prevent="drop"
          @dragover.prevent
        ></div>
      </div>
    </div>

    <div class="row auto-height right">
      <button class="btn btn-primary auto-height" v-on:click="exportData(rows, columns)">Save</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    rows: {
      type: Number,
      default: 4
    },
    columns: {
      type: Number,
      default: 4
    }
  },
  methods: {
    exportData: (rows, columns) => {
      let json = {};
      for (let row = 1; row <= rows; row++) {
        for (let column = 1; column <= columns; column++) {
          let id = "cell-" + row + "-" + column;
          let element = document.getElementById(id);
          let entity = element.getAttribute("data-entity");
          if (!json[row]) {
            json[row] = {};
          }
          json[row][column] = entity;
        }
      }
      console.log(json);
    },
    drop: e => {
      const target = e.target;
      const childCount = target.children.length;
      if (childCount <= 0) {
        const entityId = e.dataTransfer.getData("entity");
        const element = document.getElementById(entityId);
        target.appendChild(element);
        element.classList.remove("auto-height");
      } else {
        alert("You already have an entity in that field!");
      }
    }
  }
};
</script>