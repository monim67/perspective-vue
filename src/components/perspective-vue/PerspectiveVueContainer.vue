<template>
  <div class="perspective-vue-container">
    <img :src="config.background" alt="3D football field">
    <PerspectiveVueElement
      v-for="(element, index) in config.elements" v-bind:key="index"
      :container="container"
      :element="element"
      />
  </div>
</template>

<script>
import PerspectiveVueElement from "./PerspectiveVueElement.vue";

export default {
  name: "PerspectiveVueContainer",
  components: {
    PerspectiveVueElement
  },
  props: {
    config: Object
  },
  computed: {
    container: function() {
      var props = {
        origin: this.config.bottomLeftCorner
      };
      props.b = this.config.topRightCorner.x - this.config.topLeftCorner.x;
      props.a =
        props.b +
        2 * (this.config.topLeftCorner.x - this.config.bottomLeftCorner.x);
      props.h = this.config.bottomLeftCorner.y - this.config.topLeftCorner.y;
      props.p = props.a * props.h / (props.a - props.b);
      return props;
    }
  }
};
</script>

<style scoped>
.perspective-vue-container {
  position: relative;
  width: 743px;
  margin: auto;
}
</style>
