<template>
	<article class="app-teams">
		<app-teams-team-block
			v-for="(team, key) in teamList"
			:key="key"
			:thumbnail="team.thumb"
		>
			<template #title>{{ team.title }}</template>
			<template #desc>{{ team.desc }}</template>
		</app-teams-team-block>
	</article>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
// Components //
import AppTeamsTeamBlock from "@/components/app/teams/team-block.vue";

@Component({
	components: {
		AppTeamsTeamBlock
	}
})
export default class AppTeams extends Vue {
	teamList = {
		"app:ple-pie": {
			thumb: "about-1.jpg",
			title: "앱 만들기",
			desc: "우리 함께 만들어보아요..앱!"
		},
		"republic-of-game": {
			thumb: "about-1.jpg",
			title: "게임 만들기",
			desc: "우리 함께 만들어보아요..게임!"
		},
		"iwop": {
			thumb: "about-1.jpg",
			title: "웹 만들기",
			desc: "우리 함께 만들어보아요..웹!"
		},
		"zer0pen": {
			thumb: "about-1.jpg",
			title: "게임 만들기 2",
			desc: "우리 함께 만들어보아요..게임@"
		},
		"ana": {
			thumb: "about-1.jpg",
			title: "서버 만들기",
			desc: "우리 함께 만들어보아요..서버!"
		},
		"edcan": {
			thumb: "about-1.jpg",
			title: "앱 만들기",
			desc: "우리 함께 만들어보아요..앱@"
		},
		"blro": {
			thumb: "about-1.jpg",
			title: "강경태",
			desc: "안녕하세요 :D"
		}
	}
}
</script>

<style lang="scss" scoped>
@import "../../assets/variables";

.app-teams {
	display: grid;

	grid-template-columns: repeat(4, 1fr);
}
</style>
