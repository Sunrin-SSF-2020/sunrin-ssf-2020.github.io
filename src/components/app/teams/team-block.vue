<template>
	<div
		class="app-teams-team-block"
		@click="changeShowPopup(true)"
		@keydown.enter.prevent="onEnter"
		@keydown.esc.prevent="onEsc"
	>
		<div
			tabindex="0"
			:class="cardClasses"
			@focus="onFocus"
			@blur="onBlur"
		>
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
				<div class="img" :style="backStyle">{{ description }}</div>
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
							<span class="heading">수업계획</span>
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
					:tabindex="showPopup ? 0 : -1"
					class="close"
					@click.prevent.stop="changeShowPopup(false)"
					@focus="onFocusClose"
					@blur="onBlurClose"
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

	isFocus: boolean = false;
	isFocusClose: boolean = false;
	showPopup: boolean = false;

	changeShowPopup(show: boolean) {
		this.showPopup = show;
		document.body.style.overflowY = show ? "hidden" : "auto";
	}

	onFocus() {
		this.isFocus = true;
	}
	onBlur() {
		this.isFocus = false;
	}
	onFocusClose() {
		this.isFocusClose = true;
	}
	onBlurClose() {
		this.isFocusClose = false;
	}

	onEnter() {
		if (this.isFocusClose) this.changeShowPopup(false);
		else if (this.isFocus) this.changeShowPopup(true);
	}
	onEsc() {
		if (this.showPopup) this.changeShowPopup(false);
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
	&:focus,
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

	transition: opacity 0.2s;

	pointer-events: none;

	.content {
		display: flex;
		gap: 64px;
		padding: 32px;

		height: 100%;
		max-height: 512px + 64px;
		overflow-y: auto;

		position: relative;

		background-color: #ffffff;

		.img {
			flex-shrink: 0;

			width: 512px;
			height: 100%;

			background-size: contain;
			background-repeat: no-repeat;

			font-size: 0;
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
				font: {
					family: "GoyangDeogyang", sans-serif;
					size: 28px;
					weight: 600;
				}
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
					display: inline-block;
					width: 48px;

					color: #182860;
					font: {
						family: "GoyangDeogyang", sans-serif;
						weight: 600;
					}
				}
			}
		}

		.close {
			display: none;

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

	&.show {
		opacity: 1;
		pointer-events: all;

		.close {
			display: flex;
		}
	}
}

@media screen and (max-width: 1024px) {
	.popup {
		.content {
			flex-direction: column;

			width: fit-content;
			max-height: 100%;
			margin: 0 auto;

			.img {
				width: 100%;
				max-width: 300px;
				height: 300px;
				margin: 0 auto;
			}
			.contents {
				width: fit-content;
				margin: 0 auto;
			}
		}
	}
}
@media screen and (max-width: 364px) {
	.popup {
		.content {
			gap: 0;
			padding: 0;

			.img {
				position: relative;

				width: 100vw;
				max-width: 100vw;
				height: 100vw;
			}
			.contents {
				padding: 32px;

				.flex {
					flex-direction: column;
				}
			}
		}
	}
}
</style>
