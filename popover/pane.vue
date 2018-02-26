<template>
    <transition :enter-class="enterClass"
                :leave-active-class="leaveActiveClass">
        <div class="tab" v-show="curIndex === tabIndex">
            <slot></slot>
        </div>
    </transition>
</template>

<script>

export default {
  props: {
    curIndex: {
      type: Number,
      default: 0
    }
  },

  data() {
    return {
      tabIndex: 0,
      enterClass: "",
      leaveActiveClass: ""
    };
  },

  created() {
    const self = this;
    this.$parent.$on("tabIndexChange", function(prevIndex, tabIndex) {
      self.tabIndex = tabIndex;
      if (tabIndex > prevIndex) {
        self.enterClass = "offset-right";
        self.leaveActiveClass = "offset-left v-leave-active";
      } else {
        self.enterClass = "offset-left";
        self.leaveActiveClass = "offset-right v-leave-active";
      }
    });
  }
};
</script>

<style lang="css" scoped>
.tab {
  position: absolute;
  overflow: hidden;
  width: 100%;
  top: 0;
  left: 0;
  bottom: 0;
}
</style>
