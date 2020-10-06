<template>
	<article class="app-about" id="about">
		<app-about-panel
			background="#f9f9ff"
		>
			<div class="content">
				<h1 class="heading">2020 소프트웨어 나눔축제</h1>
				<span class="subheading">We are here to listen from you deliver exellence</span>
				<p class="paragraph">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore. magna aliqua. Ut enim ad minim. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore. magna aliqua. Ut enim ad minim.</p>
			</div>
			<img
				src="@/assets/about-1.jpg"
				alt="개요 사진 1"
				class="image"
			>
		</app-about-panel>
		<app-about-panel
			text="white"
			background="#222222"
			:imagesize="0.6"
		>
			<img
				src="@/assets/about-2.jpg"
				alt="개요 사진 2"
				class="image"
			>
			<div class="content">
				<span class="tag">24/7 SUPPORT SYSTEM</span>
				<h1 class="heading">We Telecast our Coffee Making Live</h1>
				<span class="subheading">We are here to listen from you deliver exellence</span>
				<p class="paragraph">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore. magna aliqua. Ut enim ad minim. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore. magna aliqua. Ut enim ad minim.</p>
			</div>
		</app-about-panel>
	</article>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
// Components //
import AppAboutPanel from "@/components/app/about/panel.vue";

@Component({
	components: {
		AppAboutPanel
	}
})
export default class AppAbout extends Vue {}
</script>

<style lang="scss" scoped>
@import "../../assets/variables";

.app-about {
	color: $text-color-title;
}
</style>
