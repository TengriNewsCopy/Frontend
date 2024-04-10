<script>
import axios from "axios";

export default {
  name: "NewsPage",
  data() {
    return {
      result: [],

      tags: []
    };
  },
  methods: {
    async getNews() {
      const { data } = await axios.get("http://8.219.172.134/api/news/" + this.$route.params.id);
      this.result = data.data;
      this.result.published_at = new Intl.DateTimeFormat('default', {dateStyle: 'long'}).format(new Date(this.result.published_at));
    },
    async getTags() {
      const {data} = await axios.get("http://8.219.172.134/api/tags");

      this.tagsList = data;
    }
  },
  beforeMount() {
    this.getNews();
    this.getTags();
  },
};
</script>

<template>
  <div class="news-article">
    <p class="news-date">{{result.published_at}}</p>
    <p class="news-title">{{result.title}}</p>
    <div class="divider"></div>
    <div class="news-data">
      <img src="../assets/images/logo_long.svg" alt="">
      <p>{{result.views}}</p>
      <img src="../assets/images/circle-comments.svg" alt="">
      <p>{{result.comments.length}}</p>
      <img src="../assets/images/circle-share.svg" alt="">
    </div>
    <div class="news-parent-container">
      <div class="news-container" v-html="result.content"></div>
      <div class="sidebar">
        <p class="sidebar-item-title">TENGRI AUTO</p>
        <div class="divider"></div>
        <div class="sidebar-item">
          <p class="sidebar-item-content"><a href="#">BMW провел испытания в ледяных условиях для своих прототипов. Видео</a></p>
          <div class="sidebar-item-data">
            <p class="sidebar-item-date">Сегодня</p>
            <img src="../assets/images/logo_long.svg" alt="">
            <p>1437</p>
          </div>
        </div>
        <div class="divider"></div>
        <div class="sidebar-item">
          <p class="sidebar-item-content"><a href="#">Огромную яму на дороге в Айнабулак сняли на видео</a></p>
          <div class="sidebar-item-data">
            <p class="sidebar-item-date">Сегодня</p>
            <img src="../assets/images/logo_long.svg" alt="">
            <p>4069</p>
            <img src="../assets/images/circle-comments.svg" alt="">
            <p>3</p>
          </div>
        </div>
        <div class="divider"></div>
        <div class="sidebar-item">
          <p class="sidebar-item-content"><a href="#">Электрический "Гелендваген" дебютирует на Пекинском автосалоне в апреле. Видео</a></p>
          <div class="sidebar-item-data">
            <p class="sidebar-item-date">Сегодня</p>
            <img src="../assets/images/logo_long.svg" alt="">
            <p>6273</p>
            <img src="../assets/images/circle-comments.svg" alt="">
            <p>5</p>
          </div>
        </div>
      </div>
    </div>
    <div class="site-section">
      <ul class="news-list">
        <li v-for="t in tagsList?.data?.slice(0, 8)" class="news-icon"><a @click="tags=t" href="#">{{ t }}</a></li>
      </ul>
    </div>
  </div>
</template>

<style>

</style>
