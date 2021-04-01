<template>
  <div id="app">

    <!-- route outlet -->
    <router-view></router-view>
    <ul>
      <!-- use router-link component for navigation. -->
      <!-- speccify the link by passing the `to` prop. -->
      <!-- `<router-link>` will be rendered as an `<a>` tag by default -->
      <li v-if="$router.currentRoute.path == '/login' || $router.currentRoute.path == '/'"><router-link to="/login"  >Login</router-link></li>
      <li v-if="$router.currentRoute.path != '/login' && $router.currentRoute.path != '/'"><router-link to="/new" >New Item</router-link></li>
      <li v-if="$router.currentRoute.path != '/login' && $router.currentRoute.path != '/'"><router-link to="/newOld" >New Item Old(Alpha Version)</router-link></li>

      <li v-if="false"><router-link to="/item/:id" >Item</router-link></li>
      <li v-if="false"><router-link to="/thanks" >Thanks</router-link></li>
      <li v-if="$router.currentRoute.path != '/login'  && $router.currentRoute.path != '/'"><router-link to="/browse" >Browse</router-link></li>
      <li v-if="$router.currentRoute.path != '/login'" @click="onLogoutClick()" > <router-link to="/login" >Logout</router-link></li>

    </ul>
  </div>
</template>

<script>
  import Vue from 'vue';
  import login from "@/components/login";
  import itemUpload from "@/components/itemUpload";
import thanks from "@/components/thanks";
import browse from "@/components/browse";
import newItem from "@/components/newItem";
import item from "@/components/item";
import VueRouter from 'vue-router';

Vue.use(VueRouter);

const routes = [
  {path: '/login', component: login, meta: {guest: true}},
  // {path: '/verify', component: verify},
  {path: '/new', component: itemUpload, meta: {requiresAuth: false}},

  {path: '/item/:id', component: item, meta: {requiresAuth: true}},
  {path: '/thanks', component: thanks, meta: {requiresAuth: true}},
  {path: '/newOld', component: newItem, meta: {requiresAuth: true}},
  {path: '/browse', component: browse, meta: {requiresAuth: true}}
];

const router = new VueRouter({
  routes,
  mode: 'history'
});

// restricts access based on jwt token

router.beforeEach((to, from, next) => {

  // Login session expire in 1 hour
  var now = new Date().getTime();
  var time = localStorage.getItem('expire');
  console.log('time' + time);
  if (time === null){
    localStorage.clear();
  }else {
    if(now - time > 15*60*1000) {     // 60*60*100 = 1 hour
      localStorage.clear();
    }
  }


    if(to.matched.some(record => record.meta.requiresAuth)) {
        if (localStorage.getItem('jwt') == null) {
            next({
                path: '/login',
                params: { nextUrl: to.fullPath }
            })
        } else {
            next();
        }
    } else if(to.matched.some(record => record.meta.guest)) {
      if(localStorage.getItem('jwt') == null){
            next()
        }
        else{
            next({ path: '/browse'})
        }
    } else {
        next() 
    }
});

export default {
  router,
  methods:{
    onLogoutClick(){
      localStorage.clear();
      console.log("session cleared, logged out! ");
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
