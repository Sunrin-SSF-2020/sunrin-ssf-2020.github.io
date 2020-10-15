<template>
	<article class="app-main" id="main">
		<span class="slogan">소프트웨어의 미래를 만나보세요</span>
		<h1 class="title">2020 소프트웨어 나눔축제</h1>
		<span class="timer">
			신청마감
			<span class="d-day">{{ dDay }}</span>
		</span>
		<!-- Info -->
		<span class="info calendar">
			<app-icon icon="mdi-calendar"/>
			2020년 08월 31일
		</span>
		<span class="info address">
			<app-icon icon="mdi-map-outline"/>
			서울특별시 용산구 원효로 97길 33-4 선린인터넷고등학교
		</span>
	</article>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";
// Components //
import AppIcon from "@/components/app/icon.vue";

@Component({
	components: {
		AppIcon
	}
})
export default class AppMain extends Vue {
	now: Date | null = null;
	end: Date = new Date("2020-10-26");

	created() {
		fetch("http://worldtimeapi.org/api/timezone/Asia/Seoul").then((response) => {
			if (response.ok) {
				return response.json();
			}
			throw new Error("World time api error!");
		}).then((json) => {
			this.now = new Date(json.datetime);
		});
	}

	get dDay(): string {
		if (!this.now) return "-";

		let date = Math.floor((this.end.getTime() - this.now.getTime()) / 1000 / 60 / 60 / 24);
		if (date > 0) {
			return `D-${date}`;
		} else if (date == 0) {
			return "D-DAY";
		} else {
			return ""
		}
	}
}
</script>

<style lang="scss" scoped>
@import "../../assets/variables";

.app-main {
	display: flex;
	height: 100vh;

	flex-direction: column;

	justify-content: center;
	align-items: center;

	background: {
		image: url("../../assets/banner-main.jpg");
		color: rgba(4, 9, 30, 0.85);

		blend-mode: overlay;

		position: center;
		size: cover;
	}

	color: #ffffff;

	.slogan {
		color: $theme-color;
		font-size: 22px;
	}
	.title {
		margin: {
			top: 8px;
			bottom: 48px;
		}

		font-family: "GoyangDeogyang", sans-serif;
		font-size: 64px;
	}
	.timer {
		margin-bottom: 32px;

		font: {
			size: 22px;
			weight: 600;
		}

		.d-day {
			color: $theme-color;
		}
	}
	.info {
		display: flex;

		margin-bottom: 12px;

		align-items: center;
		gap: 12px;

		font-size: 18px;

		.app-icon {
			color: $theme-color;
			font-size: 24px;
		}
	}
}
</style>
