<template>
  <div>
    <div class="preview">
      <DropdownComponent>
        <button @click="addToCart">Add to cart!</button>
        <div>
          preview
        </div>
      </DropdownComponent>
    </div>
    <div class="top-row">
      <PartSelector :parts="availableParts.heads"
        position="top"
        @selectedPartEvent="part => selectedRobot.head=part"/>
    </div>
    <div class="middle-row">
      <PartSelector :parts="availableParts.arms"
        position="left"
        @selectedPartEvent="part => selectedRobot.leftArm=part"/>
      <PartSelector :parts="availableParts.torsos"
        position="center"
        @selectedPartEvent="part => selectedRobot.torso=part"/>
      <PartSelector :parts="availableParts.arms"
        position="right"
        @selectedPartEvent="part => selectedRobot.rightArm=part"/>
    </div>
    <div class="bottom-row">
      <PartSelector :parts="availableParts.bases"
        position="bottom"
        @selectedPartEvent="part => selectedRobot.base=part"/>
    </div>
    <table>
      <tr v-for="(robot, idx) in cart" :key="idx">
        <td>{{idx}}</td>
        <td>{{robot.head.title}}</td>
        <td>{{robot.cost}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import availableParts from '../data/parts';
import PartSelector from './PartSelector.vue';
import DropdownComponent from '../shared/DropdownComponent.vue';

export default {
  name: 'RobotBuilder',
  components: { PartSelector, DropdownComponent },
  data() {
    return {
      availableParts,
      cart: [],
      selectedRobot: {
        head: {},
        leftArm: {},
        rightArm: {},
        torso: {},
        base: {},
      },
    };
  },
  methods: {
    addToCart() {
      const robot = this.selectedRobot;
      const cost = robot.head.cost
        + robot.leftArm.cost
        + robot.torso.cost
        + robot.rightArm.cost
        + robot.base.cost;
      this.cart.push(Object.assign({}, robot, { cost }));
    },
  },
};
</script>

<style scoped>
.part {
  position: relative;
  width:165px;
  height:165px;
  border: 3px solid #aaa;
}
.preview {
  display:flex;
  justify-content:right;
  min-width: 200px;
}
.top-row {
  display:flex;
  justify-content: space-around;
}
.middle-row {
  display:flex;
  justify-content: center;
}
.bottom-row {
  display:flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector, .center .next-selector {
  opacity:0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
</style>>
