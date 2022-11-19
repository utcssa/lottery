<template>
  <div class="flex h-screen bg-center bg-no-repeat">
    <header class="absolute w-screen flex items-center justify-center pt-[5vh]">
      <img src="~/assets/logo.png" alt="logo" class="h-[15vh]" />
    </header>
    <main class="m-auto w-2/3 max-w-md min-w-fit overflow-hidden rounded-lg shadow-lg ring-1 ring-black ring-opacity-5 backdrop-blur bg-white bg-opacity-60">
      <h1 class="text-4xl text-center font-bold my-8">Lucky Draw</h1>
      <DigitDisplay
        class="my-8"
        :target="dispNum"
        @animation-start="loading = true"
        @animation-end="onAnimationEnd()"
      />
      <div class="flex justify-center my-8">
        <button
          @click="draw()"
          :disabled="loading"
          :class="{
            'bg-gray-300': loading,
            'bg-red-500 hover:bg-red-600 active:bg-red-700 active:shadow-inner shadow-md': !loading,
          }"
          class="text-white text-xl font-medium rounded-full px-8 py-2 transition-all duration-200 disabled:cursor-wait"
        >
          {{ loading ? 'Loading...' : 'Draw' }}
        </button>
      </div>
    </main>
    <footer class="absolute bottom-4 w-screen text-center">
      <span class="text-slate-500">&copy; <strong>UTCSSA</strong> - Alex Kuang, 2022.</span>
    </footer>
  </div>
</template>

<script setup lang="ts">
const { $confetti } = useNuxtApp().vueApp.config.globalProperties
console.log(useNuxtApp().vueApp)
const dispNum = ref<number>(0)
const loading = ref<boolean>(false)

const draw = () => {
  dispNum.value = Math.floor(Math.random() * 300)
}

const onAnimationEnd = () => {
  loading.value = false
  $confetti.start({
    particlesPerFrame: 2,
    defaultDropRate: 15,
    particles: [
      { type: 'circle' },
      { type: 'heart' },
      { type: 'rect' },
    ]
  })
  setTimeout(() => {
    $confetti.stop()
  }, 2000)
}
</script>