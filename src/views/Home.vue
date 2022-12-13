<template>
  <div class="home">

			<div class="post" v-for="post in posts" :key="post._id">
					<h2>{{post.title}}</h2>
		  				<div v-for="item in post.body" :key="item._key">
				  				<img :src="imageUrlFor(item).ignoreImageParams().width(240)" alt="" v-if="item._type === 'image'"/>

									<component v-else v-for="child in item.children" :key="child._key" :is="child._type">
												{{child.text}}
									</component>
							</div>
			</div>

  </div>
</template>

<script>
// @ is an alias to /src
import {useSanityFetcher} from 'vue-sanity';
import imageUrlBuilder from "@sanity/image-url";
const imageBuilder = imageUrlBuilder({
	projectId: "pgnml2hy",
	dataset: "production"
});



export default {
  name: 'Home',
  components: {  },
		data(){
			return {
				test: ''
			}
		},
	setup() {
		const { data: posts } = useSanityFetcher('*[_type == "post"]');
		return { posts }
	},
	methods :{
		imageUrlFor(source) {
			return imageBuilder.image(source);
		}
	}
}
</script>

<style lang="scss">
.post {
  max-width: 1020px;
  display: block;
  margin: auto;
  padding: 20px;
}
</style>
