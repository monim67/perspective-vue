<template>
  <div id="app">
    <SideBar/>
    <div class="content">
      <PerspectiveVueContainer :config="pv_config"/>
      <DemoContainer :config="demo_config" v-on:positionUpdate="DemoContainer_onPositionUpdate"/>
      <p class="info-note">
        Hover the mouse pointer over the rectangular field above to move the ball.
      </p>
    </div>
  </div>
</template>

<script>
import PerspectiveVueContainer from "./components/perspective-vue/PerspectiveVueContainer.vue";
import DemoContainer from "./components/DemoContainer.vue";
import SideBar from "./components/SideBar.vue";

export default {
  name: "app",
  components: {
    PerspectiveVueContainer,
    DemoContainer,
    SideBar
  },
  data() {
    return {
      pv_config: {
        background: require("./assets/images/field-3d.png"),
        topLeftCorner: { x: 177, y: 59 },
        topRightCorner: { x: 564, y: 59 },
        bottomLeftCorner: { x: 52, y: 213 },
        elements: {
          ball: {
            image: require("./assets/images/ball.png"),
            width: 40,
            height: 40,
            position: { x: 0.5, y: 0 }
          }
        }
      },
      demo_config: {
        background: require("./assets/images/field-2d.png"),
        width: 480,
        height: 300,
        cursor: {
          image: require("./assets/images/ball-xs.png"),
          x: 12,
          y: 12
        }
      }
    };
  },
  methods: {
    DemoContainer_onPositionUpdate: function(position) {
      this.pv_config.elements.ball.position = position;
    }
  }
};
</script>

<style>
#app {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial,
    sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: white;
}
body {
  margin: 0px;
  background: rgb(11, 103, 58);
}
.side-bar {
  float: left;
  width: 340px;
}
.content {
  margin-left: 370px;
  text-align: center;
}
.info-note{
  color: yellow;
}
</style>
