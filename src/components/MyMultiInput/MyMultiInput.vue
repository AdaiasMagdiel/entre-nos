<template>
	<div ref="element" class="flex flex-col items-center justify-start w-full">
		<input
			v-for="(element, index) in inputs"
			:key="index"
			type="text" :placeholder="`Jogador ${index + 1}`"
			:class="element.visible ? classesVisible : classesPhantom"
			@keyup="(e) => handlePhantom(index, e)"
			:value="element.value ? element.value : ''"
		/>
	</div>
</template>

<script setup>
	import { ref } from 'vue';

	const classesVisible = 'w-[80%] px-4 py-2 my-2 border-4 rounded-xl text-red-500 border-red-500';
	const classesPhantom = 'w-[80%] px-4 py-2 my-2 border-4 rounded-xl text-slate-200 border-slate-200';
	const element = ref(null)
	const inputs = ref([]);


	const playersStorage = localStorage.getItem('players')
	if (playersStorage) {
		const players = JSON.parse(playersStorage)
		inputs.value = players.map(player => {
			return {visible: true, value: player}
		})
		inputs.value.push({ visible: false })
	} else {
		inputs.value = [
			{ visible: true },
			{ visible: false }
		];
	}

	function handlePhantom(index, element){
		if (index == 0) return

		if (inputs.value[index].visible == false) {
			inputs.value[index].visible = true
			inputs.value.push({visible: false})
		}

		if (element.target.value == '' && index == inputs.value.length - 2) {
			inputs.value[index] = {visible: false}
			inputs.value.pop()
		}
	}
</script>
