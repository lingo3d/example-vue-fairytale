<script setup lang="ts">
import { useKeyboard, useLoop, usePreload } from "lingo3d-vue"
import Game from "./Game.vue"
import { ref, watchEffect } from "vue"

const progress = usePreload(["fairy.glb", "idle.fbx", "person.glb", "running.fbx", "skybox.jpg"], "21.2mb")
const characterRef = ref()
const key = useKeyboard()
const running = ref(false)

const displayLoading = ref(true)

useLoop(() => {
  if (key.value === "w") {
    running.value = true
    characterRef.value.moveForward(-6)
  } else {
    running.value = false
  }
})

watchEffect(() => {
  if (progress.value > 99) {
    displayLoading.value = false
  }
})
</script>

<template>
  <div v-if="displayLoading" class="w-screen h-screen absolute bg-black text-white flex justify-center items-center">
    loading, please wait {{ progress.toFixed(2) * 100 }} %
  </div>
  <Game v-else />
</template>
