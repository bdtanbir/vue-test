<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.wrapper-box {
    max-width: 800px;
    margin: 50px auto 50px auto;
    border: 1px solid #eee;
    border-radius: 4px;
    padding: 20px;
    box-sizing: border-box;
    box-shadow: 0 0 10px rgb(0 0 0 / 4%);
}
.wrapper-box h1,
.wrapper-box h2,
.wrapper-box h3,
.wrapper-box h4,
.wrapper-box h5,
.wrapper-box h6 {
    margin: 0 0 15px 0;
    font-size: 20px;
    font-weight: 500;
}
.wrapper-box p {
    font-size: 16px;
    margin: 0 0 10px 0;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
*, *:before, *:after {
  box-sizing: border-box;
}
</style>
