<template>
  <div id="content">
    <div class="row container" style="margin: 10px;flex: 1;">
      <div class="col card" style="justify-content: space-between; flex: 12">
        <div class="row grid-container">
          <div id="grid">
            <div class="row" v-for="i in rows" :key="i">
              <div
                class="cell"
                v-for="j in columns"
                :id="'cell-' + i + '-' + j"
                :key="j"
                @dragover.prevent
              ></div>
            </div>
          </div>
        </div>
        <div class="row" style="flex:1;margin: auto">
          <button class="btn btn-primary" v-on:click="save(rows, columns)">Save</button>
          <button class="btn" v-on:click="clear(rows, columns)">Clear</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/**
 * @drop.prevent="drop"
 * @dragover.prevent
 */
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
    clear: (rows, columns) => {
      for (let row = 1; row <= rows; row++) {
        for (let column = 1; column <= columns; column++) {
          let cellId = "cell-" + row + "-" + column;
          let cell = document.getElementById(cellId);
          cell.innerHTML = "";
        }
      }
    },
    save: (rows, columns) => {
      const items = {};
      for (let row = 1; row <= rows; row++) {
        for (let column = 1; column <= columns; column++) {
          let cellId = "cell-" + row + "-" + column;
          let cell = document.getElementById(cellId);
          if (!items[row]) {
            items[row] = {};
          }

          let data = null;
          if (cell.children.length > 0) {
            try {
              data = cell.children[0].getAttribute("data-entity");
              data = JSON.parse(data);
            } catch (e) {
              data = null;
            }
          } else {
            data = null;
          }
          items[row][column] = data;
        }
      }
      console.log(items);
    }
  }
};
</script>