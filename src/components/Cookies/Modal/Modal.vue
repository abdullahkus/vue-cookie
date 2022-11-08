<script setup>
import { ref } from "vue";
import Policy from "./ScrollableText.vue";
import Settings from "./Settings.vue";
const props = defineProps(["openModal", "settings", "policyText"]);
const emit = defineEmits(["saveCookies"]);
const selectedTab = ref("Settings");

function saveHandler() {
	emit("saveCookies");
}
</script>

<template>
	<div class="relative z-10" :class="{ hidden: !props.openModal }">
		<div class="backdrop"></div>

		<div class="modal-container">
			<div class="modal-panel">
				<div class="modal">
					<div class="modal-header">
						<h3 class="text-lg">Customize Cookies</h3>
						<button @click="$emit('close')">✖</button>
					</div>
					<div class="modal-body">
						<div class="tabs-container">
							<span
								class="tab"
								:class="[
									selectedTab === 'Settings' ? 'tab-active' : 'tab-passive',
								]"
								@click="selectedTab = 'Settings'"
								>Settings</span
							>
							<span
								class="tab"
								:class="[
									selectedTab === 'Policy' ? 'tab-active' : 'tab-passive',
								]"
								@click="selectedTab = 'Policy'"
								>Cookies Policy</span
							>
						</div>
						<div class="tab-content">
							<Policy
								:policyText="props.policyText"
								v-if="selectedTab == 'Policy'"
							/>
							<Settings
								:settings="props.settings"
								@saveCookies="saveHandler"
								v-else="selectedTab == 'Settings'"
							/>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<style lang="postcss" scoped>
.backdrop {
	@apply fixed inset-0 bg-gray-600 bg-opacity-75 transition-opacity;
}
.modal-container {
	@apply fixed inset-0 z-10 overflow-y-auto;
}
.modal-panel {
	@apply flex min-h-full justify-center p-4 sm:p-0 text-center items-center sm:items-center;
}
.modal {
	@apply relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg h-[600px];
}
.modal-header {
	@apply bg-primary text-white flex justify-between p-3;
}
.modal-body {
	@apply bg-quaternary flex flex-col;
}
.tabs-container {
	@apply flex py-3 text-center;
}
.tab {
	@apply border-b-2 -mb-3 w-1/2;
}
.tab-active {
	@apply border-b-secondary text-secondary font-semibold;
}
.tab-passive {
	@apply border-b-tertiary cursor-pointer text-tertiary hover:text-secondary transition-all;
}
.tab-content {
	@apply p-3 bg-quaternary;
}
</style>
