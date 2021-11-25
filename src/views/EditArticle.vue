<template>
  <div>
    <mcv-loading v-if="isLoading"></mcv-loading>
    <mcv-article-form
      v-if="initialValues"
      :initial-values="initialValues"
      :errors="validationErrors"
      :is-submitting="isSubmitting"
      @articleSubmitting="onSubmit"
    ></mcv-article-form>
  </div>
</template>
<script>
import { mapState } from 'vuex'
import { actionTypes } from '@/store/modules/editArticle'

import McvArticleForm from '@/components/ArticleForm'
import McvLoading from '@/components/Loading'
export default {
  name: 'McvEditArticle',
  components: {
    McvArticleForm,
    McvLoading
  },
  computed: {
    ...mapState({
      isSubmitting: state => state.editArticle.isSubmitting,
      isLoading: state => state.editArticle.isLoading,
      article: state => state.editArticle.article,
      validationErrors: state => state.editArticle.validationErrors
    }),
    initialValues() {
      if (!this.article) {
        return null
      }
      return {
        title: this.article.title,
        description: this.article.description,
        body: this.article.body,
        tagList: this.article.tagList
      }
    }
  },
  mounted() {
    this.fetchArticle()
  },
  methods: {
    onSubmit(articleInput) {
      console.log({ articleInput })
      const slug = this.$route.params.slug
      this.$store
        .dispatch(actionTypes.updateArticle, { slug, articleInput })
        .then(article => {
          this.$router.push({ name: 'article', params: { slug: article.slug } })
        })
    },
    fetchArticle() {
      this.$store.dispatch(actionTypes.getArticle, {
        slug: this.$route.params.slug
      })
    }
  }
}
</script>
