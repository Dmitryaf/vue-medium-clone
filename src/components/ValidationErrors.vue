<template>
  <ul class="error-messages">
    <li v-for="errorMesage in errorsMessages" :key="errorMesage">
      {{ errorMesage }}
    </li>
  </ul>
</template>
<script>
export default {
  name: 'McvValidationErrors',
  props: {
    validationErrors: {
      type: Object,
      require: true
    }
  },
  computed: {
    errorsMessages() {
      return Object.keys(this.validationErrors).map(name => {
        const messages = this.validationErrors[name].join(', ')
        return `${name} ${messages}`
      })
    }
  }
}
</script>
