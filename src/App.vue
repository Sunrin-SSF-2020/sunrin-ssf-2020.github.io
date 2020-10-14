<template>
	<div id="app">
		<app-header/>
		<app-main class="fit" />
		<app-about class="fit" />
		<app-calendar/>
		<app-teams class="fit-top" />
		<app-footer/>
	</div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
// Components //
import AppHeader from "@/components/app/header.vue";
import AppMain from "@/components/app/main.vue";
import AppAbout from "@/components/app/about.vue";
import AppTeams from "@/components/app/teams.vue";
import AppCalendar from "@/components/app/calendar.vue";
import AppFooter from "@/components/app/footer.vue";

@Component({
	components: {
		AppHeader,
		AppMain,
		AppAbout,
		AppTeams,
		AppCalendar,
		AppFooter
	}
})
export default class App extends Vue {
	bus: Vue = new Vue();
}
</script>

<style lang="scss">
@import "./assets/variables";

body {
	margin: 0;

	font-family: sans-serif;
}

* {
	margin: 0;
	padding: 0;

	box-sizing: border-box;

	scroll-behavior: smooth;

	color: inherit;
	text-decoration: none;
	word-break: keep-all;
}

article {
	padding: 128px 0;
	&.fit,
	&.fit-top {
		padding-top: 0;
	}
	&.fit,
	&.fit-bottom {
		padding-bottom: 0;
	}

	.heading {
		margin-bottom: 16px;
		font-size: 32px;
	}
	.subheading {
		display: block;
		margin-bottom: 16px;
		font-weight: 600;
	}
	.paragraph {
		color: $text-color-desc;
		line-height: 1.5em;
	}
	.tag {
		color: $theme-color;
		font-size: 14px;
		letter-spacing: 0.2em;
	}
}
</style>
