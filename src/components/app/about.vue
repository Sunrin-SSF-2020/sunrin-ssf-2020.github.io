<template>
	<article class="app-about" id="about">
		<app-about-panel
			image="about-1.jpg"
			background="#f9f9ff"
		>
			<div class="content">
				<h1 class="heading">2020 소프트웨어 나눔축제</h1>
				<span class="subheading">소프트웨어의 미래를 만나보세요</span>
				<p class="paragraph">
					여기다가 설명을 적을겁니다<br>
					뭐라고 적을지는 모르겠어요 :(<br>
					줄 수를 채워야 해서 일단 적어둡니다 :D<br>
					하지만 이제 적을게 없네요ㅠㅜ
				</p>
			</div>
		</app-about-panel>
		<app-about-panel
			text="white"
			background="#222222"
			image="about-2.jpg"
			:imagesize="0.6"
			imagepos="left"
		>
			<div class="content">
				<span class="tag">24/7 SUPPORT SYSTEM</span>
				<h2 class="heading">We Telecast our Coffee Making Live</h2>
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
