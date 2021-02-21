<template>
  <div id="nav" class="px-4 py-2 flex justify-between bg-blue-700">
    <router-link to="/" ><button class="bg-pink-400 rounded-md text-white shadow-2xl width-4 p-2">home</button></router-link> 
    <router-link to="/about"><button class="bg-pink-400 rounded-md text-white shadow-2xl width-4 p-2">About</button> </router-link>
    
  </div>
  <router-view/>
</template>
<script>

export default {
  
}
</script>
<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
