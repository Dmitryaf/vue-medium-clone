<template>
  <div class="article-page">
    <div class="banner">
      <div v-if="article" class="container">
        <h1>{{ article.title }}</h1>
        <div class="article-meta">
          <router-link
            :to="{
              name: 'userProfile',
              params: { slug: article.author.username }
            }"
          >
            <img :src="article.author.image" />
          </router-link>
          <div class="info">
            <router-link
              :to="{
                name: 'userProfile',
                params: { slug: article.author.username }
              }"
            >
              {{ article.author.username }}
            </router-link>
            <span class="date">{{ article.createdAt }}</span>
          </div>
          <span>
            <router-link
              class="btn btn-outline-secondary btn-sm"
              :to="{ name: 'editArticle', params: { slug: article.slug } }"
            >
              <i class="ion-edit">Edit article</i>
            </router-link>
            <button class="btn btn-outline-danger btn-sm">
              <i class="ion-trash-i"></i>
              Delete article
            </button>
          </span>
        </div>
      </div>
    </div>
    <div class="container page">
      <mcv-loading v-if="isLoading"></mcv-loading>
      <mcv-error-message v-if="error"></mcv-error-message>
      <div v-if="article" class="row article-content">
        <div class="col-xs-12">
          <div>
            <p>{{ article.body }}</p>
          </div>
          TAG LIST
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { actionTypes } from '@/store/modules/article'
import { mapState } from 'vuex'

export default {
  name: 'McvArticle',
  computed: {
    ...mapState({
      isLoading: state => state.article.isLoading,
      article: state => state.article.data,
      error: state => state.article.error
    })
  },
  mounted() {
    this.fetchArticle()
  },
  methods: {
    fetchArticle() {
      return this.$store.dispatch(actionTypes.getArticle, {
        slug: this.$route.params.slug
      })
    }
  }
}
</script>
