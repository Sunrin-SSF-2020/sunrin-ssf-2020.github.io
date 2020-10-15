<template>
	<div :class="appAboutPanelClass" :style="appAboutPanelStyle">
		<img :src="imageUrl" class="image" />
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
		type: String,
		default: ""
	}) image!: string;
	@Prop({
		type: Number,
		default: 0.5,
		validator: (value: number) => value > 0 && value < 1
	}) imagesize!: number;
	@Prop({
		type: String,
		default: "right",
		validator: (value: string) => ["right", "left"].includes(value)
	}) imagepos!: string;

	get imageUrl() {
		return require(`@/assets/${this.image}`);
	}
	get appAboutPanelClass() {
		return {
			"app-about-panel": true,
			"text-white": this.text === "white",
			"img-left": this.imagepos === "left",
			"img-right": this.imagepos === "right"
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
	position: relative;

	width: 100%;
	height: fit-content;

	.content {
		width: calc(100% - var(--image-size, 50%));
		padding: 48px 64px;
	}
	.image {
		position: absolute;

		width: var(--image-size, 50%);
		height: 100%;
		object-fit: cover;
	}

	&.text-white {
		color: $text-color-white;
	}
	&.img-left {
		.content {
			margin-left: auto;
		}
		.image {
			left: 0;
		}
	}
	&.img-right {
		.content {
			margin-right: auto;
		}
		.image {
			right: 0;
		}
	}
}

@media screen and (max-width: 768px) {
	.app-about-panel {
		flex-direction: column;
	}
}
</style>
