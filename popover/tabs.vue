<template>
    <div class="tabs">
        <div class="nav">
            <div class="wrap">
                <a v-for="(item, index) in tabList" :key="item" :class="['item', {'active': tabIndex === index}]" @mouseenter="handleChangeTab(index)">{{mapList[item]}}</a>
                <div class="indicator" :style="styles"></div>
            </div>
        </div>
        <div class="content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
import Pane from "./pane.vue";
export default {
  props: {
    tabList: {
      type: Array,
      default() {
        return [];
      }
    }
  },

  data() {
    return {
      tabIndex: 0,
      mapList: {
        'us': '美国',
        'china': '中国',
        'europe': '欧洲'
      }
    };
  },

  computed: {
    styles() {
      const x = 100 * this.tabIndex;
      const length = this.tabList.length;
      return {
        width: length > 0 ? (100 / length) + '%' : '0',
        transform: "translateX(" + x + "%)"
      };
    }
  },

  methods: {
    handleChangeTab(tabIndex) {
      const prevIndex = this.tabIndex;
      this.$emit("tabIndexChange", prevIndex, tabIndex);
      this.tabIndex = tabIndex;
    }
  }
};
</script>

<style lang="css" scoped>
.tabs {
  position: relative;
  width: 100%;
  height: 100%;
}

.tabs > .nav {
  padding: 0 37px;
  height: 41px;
  box-shadow: inset 0 -1px 0 #dcdcdc;
}

.nav .wrap {
  display: table;
  width: 100%;
  height: 100%;
  position: relative;
  color: #666;
}

.nav .item {
  display: table-cell;
  height: 100%;
  vertical-align: middle;
  cursor: pointer;
  text-align: center;
  position: relative;
  z-index: 1;
}

.nav .item.active {
  color: #1482f0;
}

.nav .indicator {
  position: absolute;
  height: 100%;
  top: 0;
  left: 0;
  cursor: pointer;
  overflow: hidden;
  transition: transform 0.3s, -webkit-transform 0.3s;
  z-index: 10;
}

.nav .indicator::before {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 1px;
  border-bottom: 1px solid #1478f0;
}

.nav .indicator::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  width: 10px;
  height: 10px;
  background-color: #fff;
  border-top: 1px solid #1478f0;
  border-left: 1px solid #1478f0;
  transform: rotate(45deg) translate(-7px, 2px);
  z-index: 10;
}

.content {
  position: absolute;
  overflow: hidden;
  width: 100%;
  top: 42px;
  left: 0;
  bottom: 0;
}
</style>
