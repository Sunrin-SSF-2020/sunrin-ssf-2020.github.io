<template>
	<nav :class="classes">
		<div class="panel" />
		<button class="nav-button" @click.prevent.stop="toggleShowNav">
			<span class="bar" />
			<span class="bar" />
			<span class="bar" />
		</button>
		<div class="list">
			<a
				href="#main"
				class="nav-link"
				@click.stop="setShowNav(false)"
			>홈</a>
			<a
				href="#about"
				class="nav-link"
				@click.stop="setShowNav(false)"
			>개요</a>
			<a
				href="#calendar"
				class="nav-link"
				@click.stop="setShowNav(false)"
			>일정</a>
			<a
				href="#teams"
				class="nav-link"
				@click.stop="setShowNav(false)"
			>캠프</a>
		</div>
	</nav>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

@Component
export default class AppHeaderNav extends Vue {
	showNav: boolean = false;

	setShowNav(show: boolean) {
		this.showNav = show;
	}
	toggleShowNav() {
		this.showNav = !this.showNav;
	}

	get classes() {
		return {
			"app-header-nav": true,
			"show": this.showNav
		};
	}
}
</script>

<style lang="scss" scoped>
@import "../../../assets/variables";

.app-header-nav {
	display: flex;
	height: 100%;

	gap: 8px;

	.nav-link {
		display: inline-flex;

		height: 100%;
		padding: 0 12px;

		align-items: center;

		font-size: 12px;

		transition: color 0.1s;

		&:hover {
			color: $theme-color;
		}
	}
	.nav-button {
		display: none;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		gap: 6px;

		position: absolute;
		z-index: 4;
		top: 0;
		right: 0;

		width: 48px;
		height: 48px;
		padding: 12px;

		border: none;
		background-color: transparent;

		.bar {
			display: block;

			width: 100%;
			height: 2px;

			border-radius: 2px;

			background-color: $theme-color;

			transition: transform 0.25s;
		}
	}
	.panel {
		position: fixed;
		left: 0;
		top: 0;

		opacity: 0;

		width: 100vw;
		height: 100vh;

		background-color: rgba(#000000, 0.75);

		transition: opacity 0.25s;

		pointer-events: none;
	}

	&.show {
		.nav-button {
			.bar:first-child {
				transform: translateY(8px) rotateZ(-45deg);
			}
			.bar:nth-child(2) {
				transform: scaleX(0);
			}
			.bar:last-child {
				transform: translateY(-8px) rotateZ(45deg);
			}
		}
	}
}

@media screen and (max-width: 550px) {
	.nav-button {
		display: flex !important;
	}
	.list {
		display: flex;
		flex-direction: column;
		align-items: stretch;

		position: absolute;
		z-index: 1;
		top: 0;
		right: -80%;

		width: 75%;
		height: 100vh;
		padding-top: 48px;

		background-color: rgba(#000000, 0.9);

		transition: right 0.25s;

		.nav-link {
			height: 64px;
			padding: 0 16px;

			border-bottom: 1px dashed rgba(#ffffff, 0.1);

			color: #ffffff;
			font: {
				family: "GoyangDeogyang", sans-serif;
				size: 18px;
				weight: 600;
			}

			&:first-child {
				border-top: 1px dashed rgba(#ffffff, 0.1);
			}
		}
	}

	.app-header-nav.show {
		.list {
			right: 0;
		}
		.panel {
			opacity: 1;
		}
	}
}
</style>
