<template>
	<table class="app-calendar-table">
		<thead>
			<tr>
				<th>날짜</th>
				<th>일정</th>
				<th>세부사항</th>
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
		["10/22", "캠프 접수 시작"     , "-"],
		["10/26", "캠프 접수 마감"     , "참가자 선정 및 안내문 발송"  ],
		["10/27", "참가자 확인"           , "참가자 연락 및 참가 확인"],
		["10/31", "캠프 당일"     , "캠프 별 수업 진행"]
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
			transition: background-color 0.05s, color 0.05s;

			&:hover {
				background-color: $theme-color;
				color: $text-color-white;
			}
		}
	}
}
</style>
