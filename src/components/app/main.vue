<template>
	<article class="app-main" id="main">
		<span class="slogan">소프트웨어의 미래를 만나보세요</span>
		<h1 class="title">2020 소프트웨어 나눔축제</h1>
		<span class="timer">
			{{ dDay[0] }}
			<span class="d-day">{{ dDay[1] }}</span>
		</span>
		<!-- Info -->
		<span class="info calendar">
			<app-icon icon="mdi-calendar"/>
			캠프: 2020년 10월 31일
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
	@Prop({
		required: true
	}) now!: Date | null;
	@Prop({
		type: Array,
		required: true
	}) schedule!: { date: Date; name: string }[];

	currentSchedule: number = -1;

	get dDay(): string[] {
		if (!this.now) return ["", "-"];

		for (let i = 0; i < this.schedule.length; i++) {
			if (this.now.getTime() < this.schedule[i].date.getTime()) {
				this.currentSchedule = i;
				break;
			}
		}

		let sch = this.schedule[this.currentSchedule];
		let gap = sch.date.getTime() - this.now.getTime();
		gap = Math.round(gap / (1000 * 60 * 60 * 24));
		let result = [sch.name, ""];
		if (
			this.now.getFullYear() == sch.date.getFullYear() &&
			this.now.getMonth() == sch.date.getMonth() &&
			this.now.getDate() == sch.date.getDate()
		) {
			result[1] = "D-DAY";
		} else result[1] = `D-${gap}`;

		return result;
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
			family: "GoyangDeogyang", sans-serif;
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

@media screen and (max-width: 768px) {
	.app-main {
		.slogan {
			font-size: 18px;
		}
		.title {
			font-size: 48px;
		}
	}
}

@media screen and (max-width: 600px) {
	.app-main {
		.slogan {
			font-size: 16px;
		}
		.title {
			font-size: 32px;
		}
		.info {
			margin: 0 16px;
			align-items: flex-start;
			align-self: flex-start;

			.app-icon {
				flex-shrink: 0;
			}

			&:not(:first-child) {
				margin-top: 16px;
			}
		}
	}
}

@media screen and (max-width: 425px) {
	.app-main {
		.slogan {
			margin: 0 16px;
			align-self: flex-start;
		}
		.title {
			margin: {
				top: 8px;
				bottom: 48px;
				left: 16px;
				right: 16px;
			};
			align-self: flex-start;
		}
	}
}
</style>
