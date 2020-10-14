<template>
	<article class="app-footer" id="footer">
		<div class="links">
			<a href="#" class="link">
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

	.link {
		display: inline-flex;

		transition: color 0.1s;

		.app-icon {
			font-size: 32px;
		}

		&:hover {
			color: $theme-color;
		}
	}
}
</style>
