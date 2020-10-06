<template>
	<article class="app-calendar" id="calendar">
		<h2 class="heading">How Our Customers Treat Us</h2>
		<span class="paragraph">Who are in extremely love with eco friendly system.</span>
		<app-calendar-table/>
	</article>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
// Components //
import AppCalendarTable from "@/components/app/calendar/table.vue";

@Component({
	components: {
		AppCalendarTable
	}
})
export default class AppCalendar extends Vue {}
</script>

<style lang="scss" scoped>
@import "../../assets/variables";

.app-calendar {
	.heading {
		text-align: center;
	}
	.paragraph {
		display: block;
		margin-bottom: 64px;
		text-align: center;
	}
}
</style>
