<template>
  <transition name="fade">
    <div class="popover news-popover">
        <Tabs :tab-list="tabList">
            <Pane v-for="(tab, index) in tabList" :key="tab" :cur-index="index">
              <section>
                <article v-for="(article, index) in articles[tab]" :key="index">
                    <a>
                        <img :src="getImageUri(article.image_uri)" class="thumbnail" width="70" height="70"/>
                    </a>
                    <div class="content">
                        <h2>
                            <a>{{article.title}}</a>
                        </h2>
                        <footer>
                            <span class="time-wrap">
                                <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 1024 1024" class="icon icon-time"><path :d="timePath"></path></svg>
                                <time>{{article.display_time | formatter}}</time>
                            </span>
                            <address>
                                文 /
                                <a>{{article.author.display_name}}</a>
                            </address>
                        </footer>
                    </div>
                </article>
              </section>
            </Pane>
        </Tabs>
    </div>
  </transition>
</template>

<script>
import myMixin from "../../mixins/mixins";
import Icon from "../../../static/icon";
import Article from "../../../static/article";
import Tabs from "./tabs.vue";
import Pane from "./pane.vue";
export default {
  data() {
    return {
      timePath: Icon.time,
      tabList: [],
      articles: {}
    };
  },

  components: {
    Tabs,
    Pane
  },

  methods: {
    getImageUri(uri) {
      return uri + '?imageView2/1/w/88/h/88'
    }
  },

  mixins: [myMixin],

  filters: {
    formatter(val) {
      if (!val) { return ''; }
      const seconds = (Date.now() - val * 1000) * 0.001;
      const h = Math.floor(seconds / 3600);
      const m = Math.ceil(seconds % 3600 / 60);
      return h > 0 ? `${h}小时前`: `${m}分钟前`;
    }
  },

  created () {
    const data = Article.data;
    for(let key in data) {
      this.tabList.push(key);
    }
    this.articles = data;
  },

  mounted () {
    this.foo('1515316087')
  }
};
</script>

<style lang="css" scoped>
.popover {
  position: absolute;
  top: 100%;
  left: 50%;
  z-index: 10;
  transform: translate(-50%);
  background-color: #fff;
  box-shadow: 0 2px 6px 0 rgba(0, 0, 0, 0.4);
}

.news-popover {
  width: 380px;
  height: 240px;
}

.popover::before {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 1px;
  border-bottom: 1px solid #ccc;
}

.popover::after {
  content: "";
  position: absolute;
  top: -2px;
  left: 50%;
  width: 10px;
  height: 10px;
  border-top: 1px solid #ccc;
  border-left: 1px solid #ccc;
  background: #fff;
  transform: rotate(45deg) translate(-7px, 2px);
  z-index: 10;
}

article {
  height: 70px;
  margin: 20px 16px 20px 20px;
}

.thumbnail {
  float: left;
  margin-right: 16px;
}

.content {
  overflow: hidden;
}

h2 {
  display: inline-block;
  line-height: 1.64;
  height: 50px;
  font-size: 14px;
  font-weight: 400;
  overflow: hidden;
}

footer {
  color: #999;
  font-size: 12px;
}

.time-wrap {
  float: right;
}

.icon-time {
  width: 12px;
  height: 12px;
  vertical-align: -2px;
  fill: currentColor;
  margin-right: 6px;
}

address {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  line-height: 12px;
}

time {
  display: inline-block;
  line-height: 12px;
}
</style>
