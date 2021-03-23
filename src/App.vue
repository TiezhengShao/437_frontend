<template>
  <div id="app">

    <!-- route outlet -->
    <router-view></router-view>
    <ul>
      <!-- use router-link component for navigation. -->
      <!-- specify the link by passing the `to` prop. -->
      <!-- `<router-link>` will be rendered as an `<a>` tag by default -->
      <li><router-link to="/login">Login</router-link></li>
      <li><router-link to="/new">New Item</router-link></li>
      <li><router-link to="/item/%id">Item</router-link></li>
      <li><router-link to="/thanks">Thanks</router-link></li>
      <li><router-link to="/browse">Browse</router-link></li>
    </ul>
  </div>
</template>

<script>
import login from "@/components/login";
//import signup from "@/components/signup";
import thanks from "@/components/thanks";
import browse from "@/components/browse";
import newItem from "@/components/newItem";
import item from "@/components/item";
import Vue from 'vue';
import VueRouter from 'vue-router';

Vue.use(VueRouter);

const routes = [
  {path: '/login', component: login},
  // {path: '/verify', component: verify},
  {path: '/item/%id', component: item},
  {path: '/thanks', component: thanks},
  {path: '/new', component: newItem},
  {path: '/browse', component: browse}
];

const router = new VueRouter({
  routes,
  mode: 'history'
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
