<script setup>
import { ref } from "vue";
import TextAndSwitch from "./TextAndSwitch.vue";
import Button from "../Button.vue";
const props = defineProps(["settings"]);
const emit = defineEmits(["saveCookies"]);
let updatedSettings = ref(props.settings);
const acceptAll = ref(true);

function settingChanged(value) {
	let settingIndex = updatedSettings.value.findIndex(
		(item) => item.name === value
	);
	if (settingIndex > -1) {
		updatedSettings.value[settingIndex].status =
			!updatedSettings.value[settingIndex].status;
	}

	acceptAll.value = updatedSettings.value.every((item) => item.status);
}

function acceptAllChanged() {
	console.log(acceptAll.value);
	if (!acceptAll.value) {
		updatedSettings.value = updatedSettings.value.map((item) => ({
			...item,
			status: false,
		}));
		return;
	}
	updatedSettings.value = updatedSettings.value.map((item) => ({
		...item,
		status: true,
	}));
	return;
}

function saveHandler() {
	localStorage.setItem("cookieSettings", JSON.stringify(updatedSettings.value));
	emit("saveCookies");
}
</script>

<template>
	<div class="settings-container">
		<div class="main-switch">
			<h3>Accept All</h3>
			<label
				for="acceptall"
				class="inline-flex relative items-center cursor-pointer"
			>
				<input
					type="checkbox"
					:true-value="true"
					:false-value="false"
					id="acceptall"
					class="sr-only peer"
					v-model="acceptAll"
					@change="acceptAllChanged"
				/>
				<div
					class="w-11 h-6 bg-tertiary peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-blue-300 rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-secondary"
				></div>
			</label>
		</div>

		<div class="switch-container">
			<TextAndSwitch
				v-for="setting in updatedSettings"
				:key="setting.key"
				:setting="setting"
				@settingChanged="settingChanged"
			/>
		</div>

		<div class="settings-footer">
			<p class="text-xs">
				<a href="https://github.com/abdullahkus">Abdullah KUŞ</a> -
				<a href="https://github.com/ilkerdurmaz">İlker DURMAZ</a> -
				<a href="https://github.com/berattutumoglu">A. Berat TUTUMOĞLU</a>
			</p>
			<Button @click="saveHandler" :properties="{ title: 'Save and Accept' }" />
		</div>
	</div>
</template>

<style lang="postcss" scoped>
.settings-container {
	@apply h-[480px] flex flex-col;
}
.main-switch {
	@apply flex mb-3 justify-between text-secondary font-bold;
}
.switch-container {
	@apply overflow-auto divide-solid divide-y border-2 rounded border-secondary border-opacity-20;
}
.settings-footer {
	@apply mt-auto flex items-center justify-between;
}
</style>
