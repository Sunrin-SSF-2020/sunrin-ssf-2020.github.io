<template>
	<div class="app-teams-team-block">
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

	get thumbnailUrl() {
		return require(`@/assets/teams/front/${this.img}.png`);
	}
	get backUrl() {
		return require(`@/assets/teams/back/${this.img}.png`);
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

.app-teams-team-block {
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

	&:hover {
		.back {
			top: 0;
		}
	}
}
</style>
