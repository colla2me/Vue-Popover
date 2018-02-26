<template>
  <div>
    <div class="navbar">
        <ul class="main">
            <li
              v-for="(item, index) in dataList"
              :key="index"
              class="hoverable"
              @mouseenter.stop="item.show=true"
              @mouseleave.stop="item.show=false">
                <a>{{item.title}}</a>
                <Popover v-show="item.show"/>
            </li>
        </ul>
    </div>
  </div>
</template>

<script>
import Popover from './popover'
export default {
    data() {
        return {
            dataList: [
              {title: '资讯', show: true},
              {title: '快讯', show: false},
              {title: '行情', show: false},
              {title: '日历', show: false}
            ]
        }
    },

    components: {
        Popover
    },

    methods: {

    }
}
</script>

<style lang="css" scoped>

.navbar {
    padding: 0 30px;
    height: 60px;
    font-size: 14px;
    color: #000;
    background: hsla(0, 0%, 100%, 0.92);
    border-bottom: 1px solid #ccc;

}

.main {
  position: absolute;
  left: 50%;
  top: 0;
  transform: translateX(-50%);
  z-index: 10;
}

.main > .hoverable {
    float: left;
    position: relative;
    padding: 0 30px;
    height: 100%;
}

.hoverable > a {
    display: inline-block;
    height: 60px;
    line-height: 60px;
    cursor: pointer;
}

.hoverable a {
    transition: color 0.2s ease;
}

.hoverable a:hover {
    color: #1482f0;
}

</style>
