<template>
  <div id="nav">
    <div class="container">
    </div>

    Benkts Blog
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <router-view/>
    <Details></Details>
</template>

<script>
import Details from '@/components/Details.vue'
import { useSanityClient } from 'vue-sanity'

export default {
  name: 'HelloWorld',
	components: {
		Details
	},
	setup() {
		useSanityClient({
			projectId: 'pgnml2hy',
			dataset: 'production',
			useCdn: process.env.NODE_ENV === 'production',
		})
	},

  props: {
    msg: String
  },
}
</script>

<style>
html {
  cursor: url('/chainlightning.jpeg'), auto;
}

body {
  margin: 0;
  background: #3d3d3d;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fff;
}



#nav {
  color: #Fff;
  background-color: #4d4d4d;
  padding: 10px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
