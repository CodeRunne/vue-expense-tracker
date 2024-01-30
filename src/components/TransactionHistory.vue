<template>
	<div class="mt-3">
		<h2 class="border-b border-[#dedede] pb-[.3rem] font-bold text-lg">History</h2>
		<ul class="flex flex-col gap-y-3 py-3">
			<li 
				v-for="transaction in transactions"
				:key="transaction.id"
				class="relative flex justify-between shadow-md border-r-4 p-2 group" :class="transaction.amount < 0 ? 'border-red-400' : 'border-green-400'">
				<p class="text-md">{{ transaction.text }}</p>
				<span>{{ transaction.amount }}$</span>
				<div class="absolute -left-[9%] top-[50%] -translate-y-[50%]">
					<button @click="deleteTransaction(transaction.id)" class="bg-red-400 px-2 text-white opacity-0 group-hover:opacity-100 duration-300">
						&times;
					</button>
				</div>
			</li>
		</ul>
	</div>
</template>

<script setup>
	import { defineProps } from 'vue'
	const props = defineProps({
		transactions: {
			type: Array,
			required: true,
		},
	});

	const emit = defineEmits(['transactionDeleted'])
	const deleteTransaction = (id) => {
		emit('transactionDeleted', id)
	}
</script>