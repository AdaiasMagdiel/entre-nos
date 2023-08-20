<template>
	<button @click="handleAction" class="
	bg-white
		px-4 py-2 rounded-md
		text-red-400 text-2xl uppercase font-bold
		border-4 border-b-8 border-red-400
		active:translate-y-1 active:border-b-4
	">
		<slot></slot>
	</button>
</template>

<script setup>
	import { useRouter } from 'vue-router'

	const router = useRouter()
	const props = defineProps(['to'])

	function handleAction(){
		if(props.to === undefined) return
		router.push(props.to)
	}
</script>
