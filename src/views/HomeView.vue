<template>
  <section class="flex flex-col items-center justify-center gap-44 bg-default">
    <h1 class="text-4xl font-bold uppercase">Aquele Jogo Lá</h1>

    <MyButton :to="{name: 'players'}">Começar</MyButton>
  </section>
</template>

<script setup>
  import MyButton from '@/components/MyButton'
</script>
