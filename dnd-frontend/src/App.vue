<template>
  <div class="app-layout">
    <main class="main-content">
      <div class="container">
        <div class="card header">
          <h2>Актуальные новости {{ now }}</h2>
          <hr />
          <span class="stats">
            Открыто: <strong>{{ openRate }}</strong> | Прочитано: <strong>{{ readRate }}</strong>
          </span>
        </div>
        <app-news
          v-for="item in news"
          :key="item.id"
          :title="item.title"
          :id="item.id"
          :was-read="item.wasRead"
          v-on:open-news="openNews"
          @read-news="readEmitNews"
          @unmark="unReadNews"
        ></app-news>
      </div>
    </main>
    <Footer :companyName="'DndLab'" />
  </div>
</template>

<script>
import AppNewsVue from './AppNews.vue'
import Footer from './components/Footer.vue'

export default {
  data() {
    return {
      now: new Date().toLocaleDateString(),
      openRate: 0,
      readRate: 0,
      news: [
        {
          title: 'Новость 1',
          id: 1,
          wasRead: false,
        },
        {
          title: 'Новость 2',
          id: 2,
          wasRead: false,
        },
      ],
    }
  },
  methods: {
    openNews() {
      this.openRate++
    },
    readEmitNews(id) {
      const idx = this.news.findIndex((news) => news.id === id)
      this.news[idx].wasRead = true
      this.readRate++
    },
    unReadNews(id) {
      const news = this.news.find((news) => news.id === id)
      news.wasRead = false
      this.readRate--
    },
  },
  components: {
    'app-news': AppNewsVue,
    Footer,
  },
}
</script>

<style scoped>
.app-layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh; /* Занимает минимум всю высоту экрана */
}

.main-content {
  flex: 1; /* Растягивается, выталкивая футер вниз */
}
</style>
