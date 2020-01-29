<template>
	<div class="create">
		<form class="meme-form">
			<input name="topText" placeholder="top text" :value="this.topText" />

			<input
				name="bottomText"
				placeholder="bottomText"
				:value="this.bottomText"
			/>

			<button v-on:click="generate">New Meme</button>
			<!-- <button onClick={this.save}>Save</button> -->
		</form>

		<div class="meme" :key="this.memeKey">
			<img :src="this.memeUrl" alt="" />
			<h2 class="top">{{ this.topText }}</h2>
			<h2 class="bottom">{{ this.bottomText }}</h2>
		</div>
	</div>
</template>

<style>
@import "../meme.css";
</style>

<script>
export default {
	data: function() {
		return {
			error: "",
			memeKey: 101,
			allMemeImages: [],
			topText: "Test Text",
			bottomText: "",
			memeUrl: "http://i.imgflip.com/1bij.jpg"
		};
	},
	created: function() {
		console.log(this.memeUrl);
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
			this.memeUrl = this.allMemeImages[randNum].url;
			this.memeKey = randNum;
			console.log(this.memeUrl, this.memeKey);
		}
	}
};
</script>
