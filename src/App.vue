<script setup lang="ts">
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/core";

const greetMsg = ref("");
const name = ref("");

async function greet() {
	// Learn more about Tauri commands at https://tauri.app/develop/calling-rust/
	greetMsg.value = await invoke("greet", { name: name.value });
}
</script>

<template>
	<main class="container">
		<n-h1 class="title">Tauri + Vue 3 + TypeScript</n-h1>
		<n-p class="description">Click the button to see the magic happen!</n-p>
		<n-div class="input-group">
			<n-input v-model:value="name" placeholder="Enter your name" style="width:200px" />
			<n-button type="primary" @click="greet">Greet</n-button>
		</n-div>
		<n-alert v-if="greetMsg" type="success" show-icon>{{ greetMsg }}</n-alert>
		<n-p class="footer">Edit <n-code>src/App.vue</n-code> to test hot reloading.</n-p>
	</main>
</template>