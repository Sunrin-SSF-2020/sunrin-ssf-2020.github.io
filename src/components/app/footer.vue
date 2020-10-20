<template>
	<article class="app-footer" id="footer">
		<div class="name-link">
			<span class="name">선린인터넷고등학교</span>
			<a
				href="http://sunrint.hs.kr/"
				target="_blank"
				class="link"
			>sunrint.hs.kr</a>
		</div>
		<div class="links">
			<a
				href="https://www.facebook.com/SSFKorea/"
				target="_blank"
				class="link"
			>
				<app-icon icon="mdi-facebook" />
			</a>
		</div>
	</article>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
// Components //
import AppIcon from "@/components/app/icon.vue";

@Component({
	components: {
		AppIcon
	}
})
export default class AppFooter extends Vue {}
</script>

<style lang="scss" scoped>
@import "../../assets/variables";

.app-footer {
	padding: 64px;

	background-color: #04091e;

	color: $text-color-desc;

	.name-link {
		display: flex;
		flex-wrap: wrap;
		align-items: flex-end;
		gap: 8px;

		margin-bottom: 8px;

		.name {
			color: $text-color-white;
			font-size: large;
		}
	}
	.link {
		display: inline-flex;

		transition: color 0.1s;

		.app-icon {
			font-size: 24px;
		}

		&:hover,
		&:focus {
			color: $theme-color;
		}
	}
}
</style>
