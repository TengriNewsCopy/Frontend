<script>
import axios from "axios";

export default {
  name: "News",
  data() {
    return {
      result: [],
      page: 1,
      perPage: 2,
      search: null,
      tags: null,
      sort: 'published_at',
      order: 'desc',

      tagsList: []
    };
  },
  methods: {
    async getAnswer() {
      const { data } = await axios.get("http://8.219.172.134/api/news",
        {
                  params: {
                    search: this.search,
                    tags: this.tags,
                    page: this.page,
                    per_page: this.perPage,
                    sort: this.sort,
                    order: this.order,
                  },
              });
      this.result = data.data.data.map((item) => ({
        ...item,
        published_at: new Intl.DateTimeFormat('default', {dateStyle: 'long'}).format(new Date(item.published_at)),
      }));
    },
    async getTags() {
      const {data} = await axios.get("http://8.219.172.134/api/tags");

      this.tagsList = data;
    }
  },
  beforeMount() {
    this.getAnswer();
    this.getTags();
  },
  watch: {
    search() {
      this.getAnswer();
    },
    tags() {
      this.getAnswer();
    },
  },
};
</script>

<template>
  <div class="news-window">
    <div class="news-grid">
      <div class="site-section">
        <h1 class="section-title">Новости</h1>
        <ul class="news-list">
          <li v-for="t in tagsList?.data?.slice(0, 8)" class="news-icon"><a @click="tags=t" href="#">{{ t }}</a></li>
        </ul>
      </div>
      <div class="divider"></div>
      <div class="news-big-container">
        <div class="news-container-1">
          <div
              class="news-item"
              style="cursor: pointer"
              v-for="news in result"
              :key="news.id"
              @click="this.$router.push({ name: 'NewsPage', params: { id: news.id } })"
          >
            <img :src="news.image"  class="news-image-main" alt="">
            <div class="news-text">
              <p v-html="news.title"></p>
              <p>{{news.published_at}}</p>
              <p>{{ ' ' + news.views + ' ' + news.comments.length}}</p>
            </div>
          </div>
        </div>
        <div class="news-container-2">
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
      </div>
    </div>
  </div>
</template>
