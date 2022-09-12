<template>
  <div id="app">
    <h2>Vue.js WebSocket Tutorial</h2> 
    <input type="text" v-model="websocket_server">
  </div>
</template>

<script>
export default {
  name: 'WebSocket',
  data: function() {
    return {
      connection: null,
      websocket_server: 'ws://localhost:8080',
    }
  },
  created: function() {
    console.log("Starting connection to WebSocket Server")
    this.connection = new WebSocket(this.websocket_server);

    this.connection.onmessage = function(event) {
      console.log(event);
    }

    this.connection.onopen = function(event) {
      console.log(event)
      console.log("Successfully connected to the echo websocket server...")
      this.send("Hello from the client!")
    }
    this.connection.onerror = function(event) {
      console.log(event)
    }
    this.connection.onclose = function(event) {
      console.log(event)
    }

  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>