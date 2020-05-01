<template>
  <div id="app">
    <Sidebar>
      <div class="col">
        <div class="card">
          <label>Rows</label>
          <input v-model.number="rows" />
        </div>
      </div>
      <div class="col">
        <div class="card">
          <label>Cols</label>
          <input v-model.number="columns" />
        </div>
      </div>
    </Sidebar>
    <Content :rows="rows" :columns="columns" />
  </div>
</template>

<script>
import Sidebar from "./components/Sidebar";
import Content from "./components/Content";
export default {
  data: () => {
    return { rows: 4, columns: 4 };
  },
  components: {
    Sidebar,
    Content
  }
};
</script>

<style>
@import "./assets/main.css";
</style>