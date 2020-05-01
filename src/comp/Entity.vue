<template>
  <div
    :class="draggable ? 'column' :'row auto-height'"
    :draggable="draggable"
    @dragstart="dragStart"
    @dragover.stop
    :id="id"
  >
    <div :class="draggable ? 'card padding-h-0 auto-height entity' : 'card auto-height'">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    draggable: {
      type: Boolean,
      default: false
    },
    id: {
      type: String,
      default: () => {
        var dt = new Date().getTime();
        var uuid = "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(
          /[xy]/g,
          function(c) {
            var r = (dt + Math.random() * 16) % 16 | 0;
            dt = Math.floor(dt / 16);
            return (c == "x" ? r : (r & 0x3) | 0x8).toString(16);
          }
        );
        return uuid;
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