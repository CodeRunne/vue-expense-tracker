<template>
	<div class="mt-2">
		<h2 class="border-b border-[#dedede] pb-[.3rem] font-bold text-lg">Add New Transaction</h2>
		<form action="#" @submit.prevent="addTransaction"  class="mt-3 flex flex-col gap-y-3">
			<div>
				<label for="#" class="font-bold block text-[.92rem] mb-1">Text</label>
				<input type="text" v-model="data.text" name="text" id="text" placeholder="Enter Text" class="form-control w-full border border-[#dedede] text-[.9rem] bg-transparent px-3 h-[2.5rem] rounded-sm focus:border-[purple] focus:outline-none font-inherit duration-250">
			</div>
			<div>
				<label for="#" class="font-bold block text-[.92rem] mb-1">Amount <br>(negative - expense, positive - income)</label>
				<input type="text" v-model="data.amount" name="amount" id="amount" placeholder="Enter amount..." class="form-control w-full border border-[#dedede] text-[.9rem] bg-transparent px-3 h-[2.5rem] rounded-sm focus:border-[purple] focus:outline-none font-inherit duration-250">
			</div>
			<div>
				<button type="submit" class="w-full bg-[purple] hover:bg-[purple]/90 text-white py-2 text-[1.1rem] font-inherit rounded-sm">Add Transaction</button>
			</div>
		</form>
	</div>
</template>

<script setup>
	import { reactive } from 'vue'
	import { useToast } from 'vue-toastification'

	const data = reactive({
		text: null,
		amount: null
	})

	const emit = defineEmits(['transactionSubmitted'])

	const toast = useToast()

	const addTransaction = () => {
		if(!data.text || !data.amount) {
			toast.error('Both fields must be filled')
			return
		}

		// Emit data
		const transactionData = {
			text: data.text,
			amount: parseFloat(data.amount)
		}

		// Emit events with data
		emit('transactionSubmitted', transactionData)

		data.text = null
		data.amount = null
	}
</script>