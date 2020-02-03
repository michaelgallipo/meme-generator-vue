<template>
	<div class="meme">
		<img :src="this.memeUrl" alt />
		<p class="top">{{ this.topText }}</p>
		<p class="bottom">{{ this.bottomText }}</p>
	</div>
</template>

<script>
export default {
	name: "MemeImage",
	props: {
		meme: Object
	},
	watch: {
		meme: function(newVal, oldVal) {
			this.topText = newVal.topText;
			this.bottomText = newVal.bottomText;
			this.memeUrl = newVal.memeUrl;
		}
	},
	data: function() {
		console.log(this.meme);
		return {
			memeUrl: this.meme.memeUrl,
			topText: this.meme.topText,
			bottomText: this.meme.bottomText
		};
	}
};
</script>
