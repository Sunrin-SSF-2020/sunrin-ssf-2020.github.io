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
					모바일 어플리케이션, 웹 사이트 및 서버, 게임 등의 캠프에서 소프트웨어의 미래를 만나보세요.<br>
					원하는 캠프를 정한 후 정해진 기간동안 접수할 수 있습니다.<br>
					많은 신청 부탁드립니다 :)
				</p>
			</div>
		</app-about-panel>
		<app-about-panel
			text="white"
			background="#222222"
			image="about-2.jpg"
			:imagesize="0.5"
			imagepos="left"
		>
			<div class="content">
				<span class="tag">10월 21일부터 10월 25일까지</span>
				<h2 class="heading">캠프 접수 방법 및 안내</h2>
				<span class="subheading">신청 방법</span>
				<p class="paragraph">
					10월 21일부터 10월 25일까지 이 페이지 상단의 신청 버튼이나 캠프 목록의 신청 버튼을 통해 접수하실 수 있습니다.
				</p>
				<span class="subheading">접수 결과 및 인원</span>
				<p class="paragraph">
					접수 결과는 10월 27일에 개별적으로 안내되며 캠프별 인원은 10명입니다.<br>
					참가자에게는 교재가 배송되며 교육 수료 후 이수증이 발급됩니다.
				</p>
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
