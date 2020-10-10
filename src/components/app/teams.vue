<template>
	<article class="app-teams" id="teams">
		<h2 class="heading">캠프 목록</h2>
		<span class="paragraph">여기다 어떤 내용을 적을까요 선생님?</span>
		<div class="team-list">
			<app-teams-team-block
				v-for="(team, key) in teamList"
				:key="key"
				:thumbnail="team.thumb"
			>
				<template #title>{{ team.title }}</template>
			</app-teams-team-block>
			<div class="apply">신청하기</div>
		</div>
	</article>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";
// Components //
import AppTeamsTeamBlock from "@/components/app/teams/team-block.vue";

interface TeamData {
	thumb: string;
	title: string;
}

@Component({
	components: {
		AppTeamsTeamBlock
	}
})
export default class AppTeams extends Vue {
	@Prop({
		type: Vue,
		required: true
	}) bus!: Vue;

	teamList: { [key: string]: TeamData } = {
		"appple-pie": {
			thumb: "teams/appple-pie.png",
			title: "Android Studio로 계산기 앱 만들기"
		},
		"edcan": {
			thumb: "teams/edcan.png",
			title: "Android Studio로 나만의 채팅 앱 만들기"
		},
		"emotion": {
			thumb: "teams/emotion.png",
			title: "인공지능 챗봇을 이용한 선린 라이프 게임"
		},
		"iwop": {
			thumb: "teams/iwop.png",
			title: "HTML, CSS를 이용하여 FullPage 자기소개 사이트를 만들어보자"
		},
		"layer7": {
			thumb: "teams/layer7.png",
			title: "게시판 공격으로 알아보는 웹 해킹 기초"
		},
		"unifox": {
			thumb: "teams/unifox.png",
			title: "Unifox와 함께 배우는 웹 기초 with HTML, CSS"
		},
		"zer0pen": {
			thumb: "teams/zer0pen.png",
			title: "Unity로 나만의 크리쳐 만들기"
		}
	}
}
</script>

<style lang="scss" scoped>
@import "../../assets/variables";

.heading,
.paragraph {
	display: block;
	text-align: center;
}
.paragraph {
	margin-bottom: 32px;
}
.team-list {
	display: grid;
	grid-template-columns: repeat(4, 1fr);

	max-width: 1200px;
	margin: 0 auto;
}

@media screen and (max-width: 768px) {
	.team-list {
		grid-template-columns: repeat(3, 1fr);
	}
}
@media screen and (max-width: 420px) {
	.team-list {
		grid-template-columns: repeat(2, 1fr);
	}
}
</style>
