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
			<div class="img" :style="backStyle" />
			<div class="contents">
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
			</div>
		</div>
	</div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";

@Component({
	components: {}
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
	align-items: center;
	gap: 32px;

	position: fixed;
	z-index: 1024;
	top: 0;
	left: 0;

	opacity: 0;

	width: 100%;
	height: 100%;
	padding: 32px;

	background-color: rgba(#000000, 0.75);

	color: $text-color-white;

	transition: opacity 0.1s;

	pointer-events: none;

	.img {
		width: 512px;
		height: 512px;

		background-size: contain;
	}
	.contents {
		.heading {
			display: block;
			position: relative;

			width: fit-content;
			margin-bottom: 4px;
			padding: {
				left: 4px;
				right: 16px;
			};

			// color: #182860;
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
		}
	}

	&.show {
		opacity: 1;

		pointer-events: all;
	}
}
</style>
