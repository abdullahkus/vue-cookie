<script setup>
defineProps(["policyText"]);
</script>

<template>
	<div class="text-container">
		{{ policyText }}
	</div>
</template>

<style lang="postcss" scoped>
.text-container {
	@apply p-2 bg-quaternary rounded text-primary font-medium border-2 border-secondary border-opacity-20 overflow-auto h-[470px];
}
</style>
