<script setup>
const props = defineProps({
	properties: {
		type: Object,
		default: {
			title: "Text",
			textColor: "bg-secondary",
			bgColor: "text-quaternary",
		},
	},
});
const emit = defineEmits(["click"]);
const clickHandler = () => {
	emit("click", props.properties.title);
};
</script>

<template>
	<button class="button" @click="clickHandler">
		{{ props.properties.title }}
	</button>
</template>

<style lang="postcss" scoped>
.button {
	@apply whitespace-nowrap border-2 border-tertiary  rounded-lg px-3 py-1 bg-secondary text-quaternary hover:bg-tertiary hover:text-primary font-bold hover:border-quaternary col-span-1 lg:col-span-3 xl:col-span-1 transition-all flex justify-center;
}
</style>
