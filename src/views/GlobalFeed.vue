<template>
  <div class="home-page">
    <mcv-banner />
    <div class="container page">
      <div class="row">
        <div class="col-md-9">
          <mcv-feed :api-url="apiUrl" />
        </div>
        <div class="col-md-3">
          <mcv-tags />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import McvFeed from '@/components/Feed'
import McvTags from '@/components/Tags'
import McvBanner from '@/components/Banner'

export default {
  name: 'McvGlobalFeed',
  components: {
    McvFeed,
    McvTags,
    McvBanner
  },
  data() {
    return {
      apiUrl: '/articles'
    }
  }
}
</script>
