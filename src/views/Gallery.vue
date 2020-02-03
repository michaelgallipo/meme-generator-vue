<template>
	<div class="gallery">
		<button v-if="this.index > 0" v-on:click="prevImage">
			Prior Meme
		</button>
		<button v-if="this.index < this.memes.length - 1" v-on:click="nextImage">
			Next Meme
		</button>
		<button @click="$router.push({ name: 'edit', params: { meme } })">
			Edit
		</button>
		<MemeImage v-bind:meme="{ ...this.meme }" />
	</div>
</template>

<style scoped>
@import "../meme.css";
</style>

<script>
import MemeImage from "@/components/MemeImage.vue";
const axios = require("axios");
export default {
	props: ["meme"],
	components: {
		MemeImage
	},
	data: function() {
		return {
			memes: [],
			index: 0,
			meme: {}
		};
	},
	created: function() {
		axios
			.get("/api/memes")
			.then(response => {
				this.memes = response.data;
				this.meme = this.memes[this.index];
				console.log(this.meme);
			})
			.catch(error => {
				console.log(this.error);
			});
	},
	methods: {
		nextImage: function() {
			this.index++;
			this.meme = this.memes[this.index];
			console.log(this.index);
		},
		prevImage: function() {
			this.index--;
			this.meme = this.memes[this.index];
			console.log(this.index, this.meme);
		}
	}
};
</script>
