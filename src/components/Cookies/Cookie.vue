<script setup>
import { ref, onMounted } from "vue";
import Button from "./Button.vue";
import Modal from "./Modal/Modal.vue";
const props = defineProps({
	title: {
		type: String,
		default: "Default Title",
	},
	description: {
		type: String,
		default:
			"We baked some cookies that you have to accept, if you want to enjoy this website.It simply doesn't work without. In order to gather information and make improvements, we should use some third-party cookies too.Can we?",
	},
	acceptButtonTitle: {
		type: String,
		default: "Accept All",
	},
	acceptButtonTextColor: {
		type: String,
		default: "black",
	},
	acceptButtonBgColor: {
		type: String,
		default: "white",
	},
	rejectButtonTitle: {
		type: String,
		default: "Reject",
	},
	rejectButtonTextColor: {
		type: String,
		default: "white",
	},
	rejectButtonBgColor: {
		type: String,
		default: "red",
	},
	rejectButtonVisibility: {
		type: Boolean,
		default: true,
	},
	settingsButtonTextColor: {
		type: String,
		default: "white",
	},
	settingsButtonBgColor: {
		type: String,
		default: "red",
	},
	settings: {
		type: Object,
		default: {},
	},
	policyText: {
		type: String,
		default:
			"Lorem ipsum dolor sit amet consectetur adipisicing elit. Veniam, quas accusantium deleniti aliquid et recusandae dignissimos non. Delectus, nam enim placeat impedit obcaecati magnam eum. Pariatur placeat culpa nesciunt provident vitae, aperiam velit. Odio eius aperiam voluptate molestias ex impedit mollitia architecto amet incidunt id, voluptatum voluptates deserunt, minus repellat.",
	},
});

const cookieSettings = ref(false);

const acceptButtonProperties = {
	title: props.acceptButtonTitle,
	textColor: props.acceptButtonTextColor,
	bgColor: props.acceptButtonBgColor,
};

const rejectButtonProperties = {
	title: props.rejectButtonTitle,
	textColor: props.rejectButtonTextColor,
	bgColor: props.rejectButtonBgColor,
};

const settingsButtonProperties = {
	title: "Settings",
	textColor: props.settingsButtonTextColor,
	bgColor: props.settingsButtonBgColor,
};

const emit = defineEmits(["buttonClick"]);

const openModal = ref(false);

function clickHandler(value) {
	if (value == settingsButtonProperties.title) {
		openModal.value = true;
		emit("buttonClick", value);
		return;
	}
	if (value == acceptButtonProperties.title) {
		cookieSettings.value = true;
		localStorage.setItem("cookieSettings", JSON.stringify(props.settings));
		emit("buttonClick", value);
		return;
	}
	if (value == rejectButtonProperties.title) {
		cookieSettings.value = true;
		let updatedSettings = structuredClone(props.settings);

		updatedSettings = updatedSettings.map((item) => ({
			...item,
			status: false,
		}));

		localStorage.setItem("cookieSettings", JSON.stringify(updatedSettings));
		emit("buttonClick", value);
		return;
	}
	return;
}

function saveHandler() {
	emit("buttonClick", "Save and Accept");
	cookieSettings.value = true;
}

onMounted(() => {
	const setting = JSON.parse(localStorage.getItem("cookieSettings")) || [];
	cookieSettings.value = setting.some((item) => item.status === true);
});
</script>

<template>
	<template v-if="!cookieSettings">
		<div class="main">
			<div class="w-full text-quaternary flex flex-col gap-y-2">
				<h3 class="text-xl font-semibold">{{ props.title }}</h3>
				<p class="break-words">
					{{ props.description }}
				</p>
			</div>

			<div
				class="button-container"
				:class="[rejectButtonVisibility ? 'grid-cols-3' : 'grid-cols-2']"
			>
				<Button :properties="acceptButtonProperties" @click="clickHandler" />
				<Button
					:properties="rejectButtonProperties"
					@click="clickHandler"
					v-if="rejectButtonVisibility"
				/>
				<Button :properties="settingsButtonProperties" @click="clickHandler" />
			</div>
		</div>

		<div>
			<Modal
				:openModal="openModal"
				@close="openModal = false"
				:settings="props.settings"
				:policyText="policyText"
				@saveCookies="saveHandler"
			/>
		</div>
	</template>
</template>

<style lang="postcss" scoped>
.main {
	@apply lg:flex  items-center gap-4 bg-primary px-5 py-3 fixed bottom-0 w-full rounded-t-xl;
}
.button-container {
	@apply grid gap-2 mt-3 lg:mt-0 lg:w-1/3;
}
</style>
