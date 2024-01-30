<template>
	<div class="my-4 flex p-3 shadow-md border border-[#dedede] justify-evenly align-center divide-x divide-[#dedede] gap-x-3">
		<div class="flex flex-col justify-center align-center">
			<p>INCOME</p>
			<h2 class="text-2xl font-bold text-[#2ecc71]">{{ incomes }}$</h2>
		</div>
		<div class="pl-5 flex flex-col justify-center align-center">
			<p>EXPENSE</p>
			<h2 class="text-2xl font-bold text-red-400">{{ expenses }}$</h2>
		</div>
	</div>
</template>

<script setup>
	import { defineProps } from 'vue'

	const props = defineProps({
		incomes: {
			type: Number,
			required: true,
		},
		expenses: {
			type: Number,
			required: true,
		}
	})
</script>