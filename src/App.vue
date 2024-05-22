<template>
  <div id="app">
    <div class="wrapper">
      <nav class="navbar">
        <ul>
          <li><router-link to="/">Home</router-link></li>
          <li><router-link to="/post">Post</router-link></li>
          <li><router-link to="/todos">Todos</router-link></li>
        </ul>
      </nav>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  margin: 0 auto;
  padding: 20px;
  max-width: 600px;
}

.wrapper {
  margin-bottom: 20px;
}

.navbar {
  background-color: #333;
  overflow: hidden;
}

.navbar ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;
}

.navbar li {
  padding: 14px 20px;
}

.navbar li a {
  color: white;
  text-decoration: none;
  display: block;
}

.navbar li a:hover {
  background-color: #575757;
}
</style>
