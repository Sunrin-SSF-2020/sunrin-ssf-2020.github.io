<template>
	<article class="app-teams" id="teams">
		<h2 class="heading">캠프 목록</h2>
		<span class="paragraph">클릭해서 수업 내용을 확인하세요</span>
		<div class="team-list">
			<app-teams-team-block
				v-for="(team, key) in teamList"
				:key="key"
				:img="key"
				:title="team.title"
				:name="team.name"
				:description="team.description"
				:materials="team.materials"
				:classes="team.classes"
			/>
			<a
				v-if="apply"
				:href="form"
				target="_blank"
				class="apply"
			>
				<span class="text">신청하기</span>
			</a>
		</div>
	</article>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";
// Components //
import AppIcon from "@/components/app/icon.vue";
import AppTeamsTeamBlock from "@/components/app/teams/team-block.vue";

@Component({
	components: {
		AppIcon,
		AppTeamsTeamBlock
	}
})
export default class AppTeams extends Vue {
	@Prop({
		type: Boolean,
		default: false
	}) apply!: boolean;
	@Prop({
		type: String,
		default: ""
	}) form!: string;

	teamList: {
		[key: string]: {
			title: string;
			name: string;
			description: string;
			materials: string[];
			classes: string[];
		}
	} = {
		"appple-pi": {
			title: "Android Studio로 계산기 앱 만들기",
			name: "App:ple Pi",
			description: "xml, java 교육을 통해 앱의 기초를 배우고 이해합니다.\n이 과정 속에서 Android Studio를 통한 하나뿐인 나만의 계산기 앱을 만들 수 있습니다.",
			materials: ["안드로이드 스튜디오(최신버전)"],
			classes: [
				"Xml 의 기초학습을 통해 예제 풀어보기",
				"Button 을 활용한 여러 기능을 알아보기",
				"나만의 계산기 만들기",
				"java를 사용하여 계산기를 구동해보기"
			]
		},
		"edcan": {
			title: "Android Studio로 나만의 채팅 앱 만들기",
			name: "EDCAN",
			description: "Android Studio와 Firebase를 활용한 실시간 단체 채팅 앱을 만듭니다.\n직접 만든 앱을 나만의 디자인과 스타일로 꾸며볼 수 있습니다.",
			materials: ["최신 버전의 Android Studio (교재에 설치 방법 안내)"],
			classes: [
				"Android Studio 기초, XML과 Java 알아보기",
				"Firebase로 로그인, 회원가입 기능 개발하기",
				"Cloud Firestore로 실시간 채팅 기능 개발하기",
				"나만의 채팅 앱 커스터마이징 하기"
			]
		},
		"emotion": {
			title: "인공지능 챗봇을 이용한 선린 라이프 게임",
			name: "Emotion",
			description: "파이썬 기본 문법을 숙지하여 간단한 코드를 작성하고 자연어 처리를 이용해 텔레그램과 인공지능을 접목해 챗봇을 만듭니다.\n이를 통해 선린라이프 게임을 제작합니다.",
			materials: ["아나콘다", "파이썬", "텔레그램"],
			classes: [
				"챗봇 제작을 위한 파이썬 기본 문법 수업",
				"게임 스토리 제작을 위한 파이썬 기본 문법 수업",
				"자연어 처리 수업",
				"제작 프로그램 시연"
			]
		},
		"iwop": {
			title: "HTML, CSS를 이용해 FullPage 자기소개를 만들어보자",
			name: "IWOP",
			description: "HTML과 CSS에 대한 기초적인 문법을 학습합니다.\nFullPage를 활용한 자기소개 사이트를 제작 및 배포할 수 있습니다.",
			materials: ["Visual Studio Code", "Git 설치"],
			classes: [
				"HTML 개념과 문법 학습하기",
				"CSS를 학습하여 웹 페이지 꾸며보기",
				"FullPage 사용법 학습하기",
				"FullPage를 이용하여 나만의 자기소개 사이트 제작 및 배포하기"
			]
		},
		"layer7": {
			title: "게시판 공격으로 알아보는 웹 해킹 기초",
			name: "Layer 7",
			description: "어렵게 느껴졌던 해킹을 쉽게 알아보고, 직접 해킹 실습을 합니다. 크롬 웹 브라우저 소프트웨어를 사용하여 웹사이트가 우리와 통신하는 방법, 웹 상에서 발생하는 취약점에 대해 공부합니다.",
			materials: ["Chrome 웹 브라우저"],
			classes: [
				"클라이언트와 서버의 통신",
				"데이터베이스와 PHP",
				"XSS, SQL 삽입 공격 등 웹사이트에서 발생할 수 있는 취약점 학습",
				"멘토들이 직접 구현한 웹사이트에 취약점 실습"
			]
		},
		"unifox": {
			title: "Unifox와 함께 배우는 웹기초 with HTML, CSS",
			name: "Unifox",
			description: "HTML5, CSS3를 사용하여 웹페이지가 어떤 방식으로 만들어지게 되는지 알아봅니다. 실습을 통하여 웹페이지 제작에 대해 배울 수 있습니다.",
			materials: [
				"Visual Studio Code",
				"Git Bash",
				"Chrome",
				"자신을 소개하는 글",
				"자신의 사진 3장 (정방향 사진 1장 필수)"
			],
			classes: [
				"HTML5, CSS3 문법 및 사용법 수업",
				"웹 페이지 만들기 수업",
				"웹 페이지 만들기 수업",
				"웹 페이지 만들기 및 Github Page를 이용한 웹 호스팅"
			]
		},
		"zer0pen": {
			title: "Unity로 나만의 크리쳐 만들기",
			name: "ZER0PEN",
			description: "Unity 엔진을 사용하여 간단한 클리커 게임을 만들어 볼 수 있습니다. 게임 개발이 진행되는 과정을 배우며 체험해 볼 수 있습니다.",
			materials: ["Unity (교재에 설치방법 기재)"],
			classes: [
				"유니티 기초",
				"씬 이동 구현하기",
				"메인, 상점 기능 구현하기",
				"애니메이션 구현 및 마무리"
			]
		}
	};
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
	gap: 16px;
}

.apply {
	display: flex;
	position: relative;
	flex-direction: column;
	justify-content: center;

	border: 32px solid #1c1c33;

	.text {
		display: block;
		position: relative;
		z-index: 1;

		width: fit-content;
		margin-bottom: 8px;
		padding: 0 4px;
		margin: 0 auto;

		color: #1c1c33;
		font: {
			family: "GoyangDeogyang", sans-serif;
			size: 24px;
			weight: 600;
		}

		&::after {
			content: "";

			display: block;

			position: absolute;
			z-index: -1;
			bottom: 0;
			left: 0;

			width: 100%;
			height: 30%;

			background-color: #ffe02c;
		}
	}
}

@media screen and (max-width: 1024px) {
	.team-list {
		grid-template-columns: repeat(3, 1fr);
	}
}
@media screen and (max-width: 720px) {
	.team-list {
		grid-template-columns: repeat(2, 1fr);
	}
}
@media screen and (max-width: 450px) {
	.team-list {
		gap: 8px;
	}
	.apply {
		border-width: 24px;

		.text {
			font-size: 16px;
		}
	}
}
</style>
