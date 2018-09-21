<template>
  <img :src="config.background" v-on:mousemove="hoverHandler" alt="2D football field"
    :style="{
      width: config.width,
      height: config.height,
      cursor: cursor
    }"/>
</template>

<script>
export default {
  name: "DemoContainer",
  props: {
    config: Object
  },
  computed: {
    cursor: function() {
      var cur = this.config.cursor;
      return cur
        ? "url(" + cur.image + ") " + cur.x + " " + cur.y + ", auto"
        : "crosshair";
    }
  },
  methods: {
    hoverHandler: function(e) {
      this.$emit("positionUpdate", {
        x: e.offsetX / this.config.width,
        y: 1 - e.offsetY / this.config.height
      });
    }
  }
};
</script>
