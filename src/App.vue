<template>
  <div id="app">
    hello medium!!
    <mcv-topbar></mcv-topbar>
    <router-view></router-view>
  </div>
</template>

<script>
import McvTopbar from '@/components/Topbar'

export default {
  name: 'McvApp',
  components: {
    McvTopbar
  }
}
</script>
