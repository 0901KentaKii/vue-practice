<template>
  <div>
    <h1>{{ message }}</h1>
    <button @click="changeMessage">メッセージを変更</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: 'こんにちは Vue!'
    }
  },
  methods: {
    changeMessage() {
      this.message = 'メッセージが変更されました!'
    }
  }
}
</script>

<style scoped>
h1 {
  color: #42b983;
}
button {
  padding: 10px 20px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:hover {
  background-color: #3aa876;
}
</style>
