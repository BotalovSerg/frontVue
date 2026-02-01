<template>
  <div class="card">
    <div class="card-header">
      <h3>{{ title }}</h3>
      <!-- <button class="btn" @click="open">{{ isOpen ? 'Закрыть' : 'Открыть' }}</button> -->
      <AppButtonVue @action="open" :text="isOpen ? 'Закрыть' : 'Открыть'"></AppButtonVue>
      <!-- <button class="btn danger" v-if="wasRead" @click="notRead">Отметить не прочитанной</button> -->
      <AppButtonVue
        v-if="wasRead"
        @action="notRead"
        text="Отметить не прочитанной"
        color="danger"
      />
    </div>
    <div v-if="isOpen" class="card-content">
      <p>
        Lorem, ipsum dolor sit amet consectetur adipisicing elit. Delectus, eius iure. Adipisci
        assumenda ducimus asperiores culpa ullam minima eos, cupiditate similique et nobis
        voluptatum. Facere quis eum adipisci temporibus cum.
      </p>
      <AppButtonVue
        v-if="!wasRead"
        :color="'primary'"
        @action="readNews"
        :text="'Прочесть новость'"
      />
    </div>
  </div>
</template>

<script>
import AppButtonVue from './AppButton.vue'

export default {
  // props: ['title'],
  // emits: ['open-news'],
  props: {
    title: String,
    id: Number,
    wasRead: Boolean,
  },
  emits: {
    'open-news': null,
    unmark: null,
    'read-news'(id) {
      if (id) {
        return true
      }
      console.warn('Нет параметра id для emit read-news')
      return false
    },
  },
  data() {
    return {
      isOpen: false,
    }
  },
  methods: {
    open() {
      this.isOpen = !this.isOpen
      if (this.isOpen) {
        this.$emit('open-news')
      }
    },
    readNews() {
      this.isOpen = false
      this.$emit('read-news', this.id)
    },
    notRead() {
      this.$emit('unmark', this.id)
    },
  },
  components: { AppButtonVue },
}
</script>
