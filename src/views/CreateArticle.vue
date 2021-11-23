<template>
  <div>
    <mcv-article-form
      :initial-values="initialValues"
      :errors="validationErrors"
      :is-submitting="isSubmitting"
      @articleSubmitting="onSubmit"
    ></mcv-article-form>
  </div>
</template>
<script>
import McvArticleForm from '@/components/ArticleForm'
export default {
  name: 'McvCreateArticle',
  components: {
    McvArticleForm
  },
  data() {
    return {
      initialValues: {
        title: '',
        description: '',
        body: '',
        tagList: []
      },
      validationErrors: null,
      isSubmitting: false
    }
  },
  methods: {
    onSubmit(data) {
      console.log(data)
    }
  }
}
</script>
