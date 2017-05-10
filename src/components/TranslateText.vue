<template>
  <div class="translate-text row">
    <div class="col-md-6 col-md-offset-3 well">
      <textarea v-model="textIn" class="form-control" rows="5" cols="50"></textarea>
      <br>
      <button class="btn btn-primary btn-flat pull-right" v-on:click="Terjemahkan">Terjemahkan</button>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        textIn: ''
      }
    },
    methods: {
      Terjemahkan(e) {
        e.preventDefault()
        this.$emit('submitText', this.textIn)
      }
    }
  }
</script>
<style scoped>
</style>
