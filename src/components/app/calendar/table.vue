<template>
	<table class="app-calendar-table">
		<thead>
			<tr>
				<th>sl</th>
				<th>session</th>
				<th>speaker</th>
				<th>vanue</th>
				<th>time</th>
			</tr>
		</thead>
		<tbody>
			<tr
				v-for="(row, index) in tableBody"
				:key="index"
			>
				<template
					v-for="(sell, index) in row"
				>
					<th :key="index" v-if="index === 0">{{ sell }}</th>
					<td :key="index" v-else>{{ sell }}</td>
				</template>
			</tr>
		</tbody>
	</table>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

@Component
export default class AppCalendarTable extends Vue {
	tableBody: string[][] = [
		["01", "Reception & Taling Seats"     , "Isabelle Cooper"  , "3rd Hall Room", "02.00"],
		["02", "Breakfast and rest"           , "N/A"              , "4th Hall Room", "02.00"],
		["03", "Reception & Taling Seats"     , "Jane Daniel"      , "2nd Hall Room", "02.00"],
		["04", "Next generation speech"       , "Billy Barton"     , "1st Hall Room", "02.00"],
		["05", "Sppech for young people"      , "Flora Gonzales"   , "4th Hall Room", "02.00"],
		["06", "Lunch Break"                  , "N/A"              , "3rd Hall Room", "02.00"],
		["07", "Sppech for Middle aged people", "Francisco Barrett", "1st Hall Room", "02.00"]
	];
}
</script>

<style lang="scss" scoped>
@import "../../../assets/variables";

.app-calendar-table {
	margin: 0 auto;

	border-collapse: collapse;

	color: $text-color-desc;
	font-size: 14px;
	font-weight: 500;
	text-align: center;

	th, td {
		height: 48px;
		padding: 0 32px;

		border: 1px solid #dee2e6;
	}
	thead {
		text-transform: uppercase;

		th {
			border-bottom-width: 2px;
			background-color: #e9ecef;

			color: $text-color-title;
			font-weight: 600;
		}
	}
	tbody {
		tr {
			transition: background-color 0.1s, color 0.1s;

			&:hover {
				background-color: $theme-color;
				color: $text-color-white;
			}
		}
	}
}
</style>
