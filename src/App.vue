<template>
  <div id="app">
    <ul>
      <!-- use router-link component for navigation. -->
      <!-- specify the link by passing the `to` prop. -->
      <!-- `<router-link>` will be rendered as an `<a>` tag by default -->
      <li><router-link to="/login">Login</router-link></li>
<!--      <li><router-link to="/signup">Signup</router-link></li>
      <li><router-link to="/verify">Verify</router-link></li>
      <li><router-link to="/recovery">Recovery</router-link></li>-->
      <li><router-link to="/thanks">Thanks</router-link></li>
      <li><router-link to="/new-item">New Item</router-link></li>
      <li><router-link to="/browse">Browse</router-link></li>
    </ul>
    <!-- route outlet -->
    <router-view></router-view>
  </div>
</template>

<script>
import login from "@/components/login";
//import signup from "@/components/signup";
import Vue from 'vue';
import VueRouter from 'vue-router';

Vue.use(VueRouter);

const routes = [
  {path: '/login', component: login},
//  {path: '/signup', component: signup}
  // {path: '/verify', component: verify},
  // {path: '/recovery', component: recovery},
  // {path: '/item/%id', component: recovery},
  // {path: '/thanks', component: recovery},
  // {path: '/user/%id', component: user},
  // {path: '/new-item', component: newItem},
  // {path: '/browse', component: browse}
];

const router = new VueRouter({
  routes
});

export default {
  router
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
