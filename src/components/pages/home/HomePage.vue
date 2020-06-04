<template>
  <section>
    <div>
      <input type="search" v-model="hash">
      <a :href="url+'/'+hash">Search data</a>
    </div>
    <form :action="url" 
          method="post"
          @submit="getPostedDataHash">
      <button type="submit">Submit data</button>
      <textarea v-model="data" id="data-poster" cols="30" rows="10"></textarea>
    </form>
  </section>
</template>

<script>
export default {
  name: 'HomePage',
  data: () => ({
    hash: '',
    url: 'https://data-poster.herokuapp.com/data',
    data: ''
  }),
  props: {
    msg: String
  },
  methods: {
    getPostedDataHash(e) {
      e.preventDefault();
      fetch(this.url, {
        method: 'POST',
        body: JSON.stringify({
          data: this.data
        })
      })
    }
  }
}
</script>

<style scoped>
</style>
