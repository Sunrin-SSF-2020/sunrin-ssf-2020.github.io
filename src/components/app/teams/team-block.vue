<template>
	<div
		class="app-teams-team-block"
		@click="changeShowPopup(true)"
	>
		<div :class="cardClasses">
			<div
				v-text="title"
				class="front"
				:style="frontStyle"
			/>
			<div
				v-text="description"
				class="back"
				:style="backStyle"
			/>
		</div>
		<div :class="popupClasses">
			<div class="content">
				<div class="img" :style="backStyle" />
				<div class="contents">
					<span class="title">{{ title }}</span>
					<div class="flex">
						<div class="section materials">
							<span class="heading">준비물</span>
							<ul class="list">
								<li
									v-for="text in materials"
									:key="text"
									v-text="text"
									class="item"
								/>
							</ul>
						</div>
						<div class="section classes">
							<span class="heading">수업 일정</span>
							<ol class="list">
								<li
									v-for="(cls, index) in classes"
									:key="`${index}_${cls}`"
									class="item"
								>
									<span class="list-index">{{ index + 1 }} 차시</span>
									{{ cls }}
								</li>
							</ol>
						</div>
					</div>
				</div>
				<button
					class="close"
					@click.prevent.stop="changeShowPopup(false)"
				>
					<app-icon icon="mdi-close" />
				</button>
			</div>
		</div>
	</div>
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
export default class AppTeamsTeamBlock extends Vue {
	@Prop({
		type: String,
		required: true
	}) img!: string;
	@Prop({
		type: String,
		required: true
	}) title!: string;
	@Prop({
		type: String,
		required: true
	}) name!: string;
	@Prop({
		type: String,
		required: true
	}) description!: string;
	@Prop({
		type: Array,
		required: true
	}) materials!: string[];
	@Prop({
		type: Array,
		required: true
	}) classes!: string[];

	showPopup: boolean = false;

	changeShowPopup(show: boolean) {
		this.showPopup = show;
		document.body.style.overflow = show ? "hidden" : "hidden auto";
	}

	get thumbnailUrl() {
		return require(`@/assets/teams/front/${this.img}.png`);
	}
	get backUrl() {
		return require(`@/assets/teams/back/${this.img}.png`);
	}

	get cardClasses() {
		return {
			"card": true,
			"selected": this.showPopup
		};
	}
	get popupClasses() {
		return {
			"popup": true,
			"show": this.showPopup
		};
	}
	get frontStyle() {
		return {
			"background-image": `url(${this.thumbnailUrl})`
		};
	}
	get backStyle() {
		return {
			"background-image": `url(${this.backUrl})`
		};
	}
}
</script>

<style lang="scss" scoped>
@import "../../../assets/variables";

.app-teams-team-block{
	position: relative;
}

.card {
	position: relative;

	padding-top: 100%;

	overflow: hidden;

	cursor: pointer;

	> * {
		position: absolute;
		top: 0;
		left: 0;

		width: 100%;
		height: 100%;

		background-size: cover;

		font-size: 0;
	}

	.back {
		top: 100%;
		transition: top 0.35s ease-in-out;
	}

	&:hover,
	&.selected {
		.back {
			top: 0;
		}
	}
}

.popup {
	display: flex;
	flex-direction: column;
	justify-content: center;

	position: fixed;
	z-index: 1024;
	top: 0;
	left: 0;

	opacity: 0;

	width: 100%;
	height: 100%;

	background-color: rgba(#000000, 0.75);
	background-repeat: no-repeat;

	transition: opacity 0.1s;

	pointer-events: none;
	
	&.show {
		opacity: 1;

		pointer-events: all;
	}

	.content {
		display: flex;
		gap: 64px;
		padding: 32px;

		position: relative;

		background-color: #ffffff;

		.img {
			flex-shrink: 0;

			width: 512px;
			height: 512px;

			background-size: contain;
			background-repeat: no-repeat;
		}

		.contents {
			z-index: 1;

			width: 100%;

			.flex {
				display: flex;
				flex-wrap: wrap;
				align-items: flex-start;
				gap: 32px;
			}

			.title {
				display: block;

				width: 100%;
				margin-bottom: 32px;
				padding-right: 64px;

				color: #182860;
				font-size: 28px;
				font-weight: 600;
			}
			.heading {
				display: block;
				position: relative;

				width: fit-content;
				margin-bottom: 8px;
				padding: {
					left: 4px;
					right: 16px;
				};

				color: #182860;
				font-size: 24px;
				font-weight: 600;

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
			.list {
				margin-left: 24px;

				.item {
					margin-bottom: 2px;
				}
			}
		}
		.classes {
			.list {
				margin-left: 8px;
				list-style: none;

				.list-index {
					color: #182860;
					font-weight: 600;
				}
			}
		}

		.close {
			display: flex;

			position: absolute;
			z-index: 8;
			top: 32px;
			right: 32px;

			width: 32px;
			height: 32px;

			border: none;
			background: none;

			font-size: 32px;

			cursor: pointer;
		}
	}
}
</style>
