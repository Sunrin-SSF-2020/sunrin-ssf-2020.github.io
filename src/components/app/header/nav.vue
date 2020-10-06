<template>
	<nav class="app-header-nav">
		<a href="#main" class="nav-link">홈</a>
		<a href="#about" class="nav-link">개요</a>
		<a href="#teams" class="nav-link">동아리?</a>
		<a href="#calendar" class="nav-link">일정</a>
	</nav>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

@Component
export default class AppHeaderNav extends Vue {}
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
}
</style>
