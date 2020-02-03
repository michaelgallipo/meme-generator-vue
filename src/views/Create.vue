<template>
	<div class="create">
		<form class="meme-form">
			<input v-model="meme.topText" placeholder="top text" />
			<input v-model="meme.bottomText" placeholder="bottom Text" />

			<button v-on:click="generate">New Meme</button>
			<button v-on:click="save">Save</button>
		</form>

		<!-- <div class="meme">
			<img :src="this.meme.memeUrl" alt />
			<h2 class="top">{{ this.meme.topText }}</h2>
			<h2 class="bottom">{{ this.meme.bottomText }}</h2>
		</div> -->
		<MemeImage v-bind:meme="{ ...this.meme }" />
	</div>
</template>

<style>
@import "../meme.css";
</style>

<script>
import MemeImage from "@/components/MemeImage.vue";
const axios = require("axios");
export default {
	// props: ["meme"],
	components: {
		MemeImage
	},
	data: function() {
		return {
			error: "",
			allMemeImages: [],
			meme: {
				topText: "",
				bottomText: "",
				memeUrl: "http://i.imgflip.com/1bij.jpg"
			}
		};
	},
	created: function() {
		fetch("https://api.imgflip.com/get_memes")
			.then(response => response.json())
			.then(response => {
				if (response.success !== true) {
					this.error = response.error_message;
					return;
				}
				this.allMemeImages = response.data.memes;
			})
			.catch(err => {
				this.error = "API ERROR";
			});
	},
	methods: {
		generate: function() {
			const randNum = Math.floor(Math.random() * this.allMemeImages.length);
			this.meme.memeUrl = this.allMemeImages[randNum].url;
			// this.meme.memeKey = randNum;
			console.log(this.meme);
		},
		save: function() {
			const params = {
				memeUrl: this.meme.memeUrl,
				topText: this.meme.topText,
				bottomText: this.meme.bottomText
			};
			axios
				.post("/api/memes", params)
				.then(response => {
					if (response.status === 200) {
						window.alert("Meme saved to database");
					}
				})
				.catch(error => {
					console.log(error);
				});
			console.log(params);
		}
	}
};
</script>
