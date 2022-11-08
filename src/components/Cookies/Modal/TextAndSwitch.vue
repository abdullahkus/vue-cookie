<script setup>
const props = defineProps(["setting"]);
</script>

<template>
	<div>
		<div class="flex justify-between gap-2 p-2">
			<span class="text-sm font-medium text-secondary">{{
				props.setting.name
			}}</span>
			<label
				:for="props.setting.name"
				class="inline-flex relative items-center cursor-pointer"
			>
				<input
					type="checkbox"
					value=""
					:checked="props.setting.status"
					@change="$emit('settingChanged', props.setting.name)"
					:id="props.setting.name"
					class="sr-only peer"
				/>
				<div
					class="w-11 h-6 bg-tertiary peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-blue-300 rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-white-100 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-secondary"
				></div>
			</label>
		</div>
	</div>
</template>

<style lang="postcss" scoped></style>
