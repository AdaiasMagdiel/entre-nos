<template>
	<div class="overflow-hidden rounded-lg">
		<p @click="$emit('close-toast')" class="
			px-4 py-2 w-full
			text-lg uppercase text-center
			text-red-500 bg-white
			border-2 border-red-500
		">
			<slot></slot>
		</p>
		<div ref="progress" class="block h-1 w-0 bg-red-400"></div>
	</div>
</template>

<script setup>
	import { defineEmits, onMounted, ref } from 'vue';

	const emit = defineEmits(['close-toast'])
	const props = defineProps({
		time: {
			type: Number,
			default: 2
		}
	})
	const progress = ref(null)
	const progressWidth = ref(0)

	onMounted(() => {
		let interval = setInterval(() => {
			if (progress.value !== null) {
				progressWidth.value++
				let width = (progressWidth.value * 10 / props.time) + 10 * props.time
				progress.value.style.width = `${width}%`
			}
		}, 100)

		setTimeout(() => {
			emit('close-toast', true)
			clearInterval(interval)
		}, props.time * 1000)
	})
</script>
