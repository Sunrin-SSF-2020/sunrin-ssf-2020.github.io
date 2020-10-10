<template>
	<div class="app-teams-team-block" :style="appTeamsTeamBlockStyle">
		<div class="content">
			<span hidden class="title">
				<slot name="title"/>
			</span>
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
	}) thumbnail!: string;

	get thumbnailUrl() {
		return require(`@/assets/${this.thumbnail}`);
	}
	get appTeamsTeamBlockStyle() {
		return {
			"background-image": `url(${this.thumbnailUrl})`
		};
	}
}
</script>

<style lang="scss" scoped>
@import "../../../assets/variables";

.app-teams-team-block {
	position: relative;

	padding-top: 100%;

	background: {
		position: center;
		size: cover;
	}

	overflow: hidden;

	.content {
		position: absolute;
		bottom: 0;

		width: 100%;

		background-color: rgba(#000000, 0.75);

		color: $text-color-white;

		transition: bottom 0.25s;

		.desc {
			display: block;
			position: absolute;

			max-width: 100%;
			padding: 0 24px;
		}
	}

	&:hover .content {
		top: 0;
	}
}
</style>
