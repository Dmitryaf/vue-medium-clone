<template>
  <div>
    <mcv-loading v-if="isLoading" />
    <mcv-error-message v-if="error" :message="error" />
    <div v-if="tags" class="sidebar">
      <p>Popular Tags</p>
      <div class="tag-list">
        <router-link
          v-for="tag in tags"
          :key="tag"
          :to="{ name: 'tag', params: { slug: tag } }"
          class="tag-default tag-pill"
          >{{ tag }}</router-link
        >
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'

import { actionTypes } from '@/store/modules/tags'

import McvLoading from '@/components/Loading'
import McvErrorMessage from '@/components/ErrorMessage'

export default {
  name: 'McvTags',
  components: {
    McvLoading,
    McvErrorMessage
  },
  computed: {
    ...mapState({
      isLoading: state => state.tags.isLodaing,
      tags: state => state.tags.data,
      error: state => state.tags.error
    })
  },
  mounted() {
    this.fetchTags()
  },
  methods: {
    fetchTags() {
      this.$store.dispatch(actionTypes.getTags)
    }
  }
}
</script>
