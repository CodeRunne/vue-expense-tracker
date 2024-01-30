<template>
	<h4 class="text-[1.4rem] font-light">Your Balance</h4>
	<h2 class="text-4xl font-semibold">{{ total }}$</h2>
</template>

<script setup>
	import { defineProps } from 'vue'
	const props = defineProps({
		total: {
			type: Number,
			required: true,
		},
	})
</script>