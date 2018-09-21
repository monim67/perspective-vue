<template>
  <img :src="element.image" class="perspective-vue-element" :style="{
    left: elementAttributes.position.x + 'px',
    top: elementAttributes.position.y + 'px',
    width: elementAttributes.size.width + 'px',
    height: elementAttributes.size.height + 'px',
  }" alt="Perspective Vue Element">
</template>

<script>
export default {
  name: "PerspectiveVueElement",
  props: {
    container: Object,
    element: Object
  },
  computed: {
    elementAttributes: function() {
      var x = this.element.position.x * this.container.a;
      var y = this.element.position.y * this.container.h;
      var y_ = y * this.container.a * this.container.h / (this.container.b * this.container.h + y * (this.container.a - this.container.b));
      var x_ = x / this.container.p * (this.container.p - y_)
      var d = y_ * this.container.a / this.container.p / 2;
      var width  = this.element.width / this.container.p * (this.container.p - y_);
      var height = this.element.height / this.container.p * (this.container.p - y_);
      return {
        position: {
          x: this.container.origin.x + d + x_ - width / 2,
          y: this.container.origin.y - y_ - height
        },
        size: {
          width: width,
          height: height
        }
      }
    }
  }
};
</script>

<style scoped>
.perspective-vue-element {
  position: absolute;
  top: 0px;
  left: 0px;
}
</style>
