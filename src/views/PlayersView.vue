<template>
	<section class="bg-default flex flex-col justify-start items-center">
		<MyTitle class="my-12">Adicionar Jogadores</MyTitle>

		<MyMultiInput ref="inputList" />

		<MyButton class="my-4" @click="handlePlayers">Jogar</MyButton>

		<MyButton :to="{name: 'home'}" class="text-sm px-2 py-1">Voltar</MyButton>

		<div class="fixed inset-x-0 bottom-0 px-4 py-8 flex flex-col items-center justify-center">
			<MyToast
			v-for="(toast, index) in toasts"
			:key="index"
			@close-toast="() => closeToast(index)">{{toast}}</MyToast>
		</div>
	</section>
</template>

<script setup>
	import { ref } from 'vue'

	import MyTitle from '@/components/MyTitle'
	import MyButton from '@/components/MyButton'
	import MyMultiInput from '@/components/MyMultiInput'
	import MyToast from '@/components/MyToast'

	const inputList = ref(null)
	const toasts = ref([])

	function handlePlayers(){
		if(inputList.value === null) return
		const element = inputList.value.$el
		const players = Array.from(element.childNodes).map(elm => {
			return elm.value
		}).filter(elm => elm !== undefined && elm !== '')

		if (players.length < 3) {
			toasts.value.push('Você precisa definir no mínimo 3 jogadores.')
		} else {
			localStorage.setItem('players', JSON.stringify(players))
			toasts.value.push(`Ok, o jogo vai começar com os seguintes jogadores: ${players.join(', ')}`)
		}
	}

	function closeToast(index){
		toasts.value = toasts.value.filter((_, idx) => idx !== index);
	}
</script>
