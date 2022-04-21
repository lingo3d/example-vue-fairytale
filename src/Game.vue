<script setup lang="ts">
import { World, Model, ThirdPersonCamera, useKeyboard, useLoop, Skybox } from "lingo3d-vue"
import { ref } from "vue"

const characterRef = ref()
const key = useKeyboard()
const running = ref(false)

useLoop(() => {
  if (key.value === "w") {
    running.value = true
    characterRef.value.moveForward(-6)
  } else {
    running.value = false
  }
})
</script>

<template>
  <World>
    <Model src="fairy.glb" :scale="20" physics="map" />
    <ThirdPersonCamera active mouseControl>
      <Model
        ref="characterRef"
        src="person.glb"
        :y="200"
        :z="-150"
        :animations="{ idleAnimation: 'idle.fbx', runningAnimation: 'running.fbx' }"
        physics="character"
        :animation="running ? 'runningAnimation' : 'idleAnimation'"
      />
    </ThirdPersonCamera>
    <Skybox texture="skybox.jpg" />
  </World>
</template>
