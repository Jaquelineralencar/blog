<template>
  <nav>
   <Navbar :logo="logo_src" :alt="app_name"/>
  </nav>
  <user :users="users"/>

  <router-view/>
  <Footer/>
</template>

<script>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';
import HomeView from './views/HomeView.vue';



export default {
  components: {
    Navbar,
    Footer,
    HomeView,
  },
}
</script>


<style>
*{
  font-family: Helvetica;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

</style>
