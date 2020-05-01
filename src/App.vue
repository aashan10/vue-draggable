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
  },
  mounted: () => {
    document.addEventListener("dragstart", event => {
      const classes = event.target.classList;
      if (classes.contains("entity")) {
        event.dataTransfer.setData("entity", event.target.id);
      }
    });

    document.addEventListener("drop", event => {
      const target = event.target;
      if (target.classList.contains("cell")) {
        const target = event.target;
        const entityId = event.dataTransfer.getData("entity");
        const element = document.getElementById(entityId);
        const newElement = element.cloneNode(true);
        const id = Math.random()
          .toString()
          .split(".")[1];
        newElement.setAttribute("id", id);
        target.appendChild(newElement);
      }
    });

    document.addEventListener("click", (event) => {
      const targetClassList = event.target.classList;
      if(targetClassList.contains("remove-entity")) {
        const entityContainer = event.target.parentNode;
        if(entityContainer.classList.contains('entity') && entityContainer.parentNode.classList.contains('cell')) {
          entityContainer.parentNode.innerHTML = '';
        }
      }
    });
  }
};
</script>

<style>
@import "./assets/main.css";
</style>