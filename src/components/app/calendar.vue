<template>
	<article class="app-calendar" id="calendar">
		<h2 class="heading">전체 일정</h2>
		<span class="paragraph">
			<!-- 여기는 어떤걸 적을까요..? -->
		</span>
		<app-calendar-table/>
	</article>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";
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
		margin-bottom: 32px;
		text-align: center;
	}
}
</style>
