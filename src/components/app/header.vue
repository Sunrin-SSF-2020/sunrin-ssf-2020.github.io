<template>
	<div class="app-header" :style="appHeaderStyle">
		<div class="container">
			<a href="#main" class="logo">
				<img
					src="@/assets/logo.png"
					alt="2020 소프트웨어 나눔축제 로고"
				>
			</a>
			<app-header-nav/>
			<a href="#" class="apply">신청하기</a>
		</div>
	</div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
// Components //
import AppHeaderNav from "@/components/app/header/nav.vue";

@Component({
	components: {
		AppHeaderNav
	}
})
export default class AppHeader extends Vue {
	scrolled: boolean = false;
	background: string = "transparent";

	created() {
		window.addEventListener("scroll", this.onScrollWindow);
		this.onScrollWindow();
	}
	beforeDestroy() {
		window.removeEventListener("scroll", this.onScrollWindow);
	}

	onScrollWindow() {
		this.scrolled = window.scrollY > 0;
	}

	get appHeaderStyle(): Record<string, string> {
		return {
			"background-color": this.scrolled ? "rgba(0, 0, 0, 0.8)" : "transparent",
			"backdrop-filter": this.scrolled ? "blur(4px)" : "none"
		};
	}
}
</script>

<style lang="scss" scoped>
@import "../../assets/variables";

.app-header {
	position: fixed;
	z-index: 512;
	top: 0;
	left: 0;
	right: 0;

	height: 48px;
	padding: 8px 16px;

	color: #ffffff;

	transition: background-color 0.25s;

	.container {
		display: flex;

		height: 100%;

		align-items: center;

		.app-header-nav {
			margin: {
				left: auto;
				right: 16px;
			}
		}
	}
	.logo {
		display: inline-flex;
		height: 100%;

		img {
			height: 100%;
		}
	}
	.apply {
		display: inline-flex;

		width: 72px;
		height: 100%;

		justify-content: center;
		align-items: center;

		border: 1px solid $theme-color;
		background-color: transparent;

		color: $theme-color;
		font-size: 12px;

		transition: background-color 0.1s, color 0.1s;

		&:hover,
		&:focus {
			background-color: $theme-color;
			color: inherit;
		}
	}
}

@media screen and (max-width: 550px) {
	.app-header {
		padding: {
			top: 8px;
			bottom: 8px;
			left: 16px;
			right: 56px;
		};
		
		.app-header-nav {
			padding: 0;
		}
	}
	.apply {
		margin-left: auto;
	}
}
</style>
