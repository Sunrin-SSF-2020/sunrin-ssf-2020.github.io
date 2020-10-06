<template>
	<span class="app-icon iconify" :data-icon="icon"/>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";

@Component
export default class AppIcon extends Vue {
	@Prop({
		type: String,
		required: true
	}) icon!: string;
}
</script>
