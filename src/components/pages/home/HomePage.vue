<template>
  <section class="wrapper">
    <div>
      <input type="number" v-model="hash" class="search-hash-input neon-text" placeholder="only valid hashes">
      <a :href="url+'/'+hash" target="_blank" class="search-hash-anchor cyber-text neon-text">Open data</a>
    </div>
    <form :action="url" 
          method="post"
          @submit="getPostedDataHash">
      <p v-if="postedDataHash || isLoading" :class="isLoading">{{postedDataHash}}</p>
      <textarea v-model="data" id="data-poster" class="submit-data submit-data-textarea neon-text"></textarea>
      <button type="submit" class="cyber-text neon-text submit-data">Submit data</button>
    </form>
  </section>
</template>

<script>

export default {
  name: 'HomePage',
  data: () => ({
    hash: '',
    url: 'https://data-poster.herokuapp.com/data',
    data: '',
    postedDataHash: '',
    isLoading: ''
  }),
  props: {
    msg: String
  },
  methods: {
    getPostedDataHash(e) {
      e.preventDefault();
      this.isLoading = 'isLoading';
      fetch(this.url, {
        method: 'POST',
        body: JSON.stringify({
          data: this.data
        })
      })
      .then(r => r.text())
      .then(hash => {
        this.postedDataHash = hash;
        this.isLoading = '';
      });
    }
  }
}
</script>

<style lang="scss">
$neon-color-1: #0ff;
html {
  --blur: 3px;
  --neon-color: #{$neon-color-1};
  --neon-light: 0 0 var(--blur) var(--neon-color);
  --cyber-font: monospace;
}
.submit-data-textarea {
  height: 290px;
  width: 290px;
}
.submit-data {
  background: transparent;
  padding: 10px;
}
.cyber-text {
  font-family: var(--cyber-font);
  letter-spacing: 5px;
  text-transform: uppercase;
}
.neon-text {
  text-shadow: var(--neon-light);
  color: var(--neon-color);
}
.search-hash-anchor {
  text-align: end;
}
.search-hash-input {
  width: 290px;
  font-family: var(--cyber-font);
  padding: 10px;
  background: transparent;
  border: 1px solid var(--neon-color);
  box-shadow: var(--neon-light), inset var(--neon-light);
  color: $neon-color-1 * 0.8;
  transition: 0.5s;
  &:focus {
    --blur: 6px;
    outline: none;
  }
}

.wrapper {
  background: #101010;
  color: #f0f0f0;
  font-family: var(--cyber-font);
  display: grid;
  min-height: 100vh;
  & > * {
    padding: 5vh;
    display: grid;
    place-content: center;
    grid-gap: 25px;
    & > * {
      display: grid;
      place-content: center;
      grid-gap: 25px;
    }
  }
}

.isLoading::before {
  content: '.';
  display: block;
  animation: loadingText 0.75s linear infinite;
}

@keyframes loadingText {
  33% {
    content: '..';
  }
  66% {
    content: '...'; 
  }
}
</style>
