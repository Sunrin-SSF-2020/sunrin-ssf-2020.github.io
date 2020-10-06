<template>
	<div :class="appAboutPanelClass" :style="appAboutPanelStyle">
		<slot/>
	</div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";

@Component
export default class AppAboutPanel extends Vue {
	@Prop({
		type: String,
		default: "black",
		validator: (value: string) => ["black", "white"].includes(value)
	}) text!: "black" | "white";
	@Prop({
		type: String,
		required: true,
		validator: (value: string) => /#[0-9a-fA-F]{6,8}/.test(value)
	}) background!: string;
	@Prop({
		type: Number,
		default: 0.5,
		validator: (value: number) => value > 0 && value < 1
	}) imagesize!: number;

	get appAboutPanelClass() {
		return {
			"app-about-panel": true,
			"text-white": this.text === "white"
		};
	}
	get appAboutPanelStyle() {
		return {
			"--image-size": `${this.imagesize * 100}%`,
			"background-color": this.background
		};
	}
}
</script>

<style lang="scss" scoped>
@import "../../../assets/variables";

.app-about-panel {
	display: flex;

	width: 100%;

	.content {
		width: calc(100% - var(--image-size, 50%));
		padding: 48px 64px;
	}
	.image {
		width: var(--image-size, 50%);
		object-fit: cover;
	}

	&.text-white {
		color: $text-color-white;
	}
}
</style>
