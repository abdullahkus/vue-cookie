<script setup>
import Cookie from "./components/Cookies/Cookie.vue";
function clickHandler(val) {
	console.log(val);
}

const cookieSettings = [
	{
		name: "Option-I",
		status: true,
	},
	{
		name: "Option-II",
		status: true,
	},
	{
		name: "Option-III",
		status: true,
	},
	{
		name: "Option-IV",
		status: true,
	},
	{
		name: "Option-V",
		status: true,
	},
];

const desc =
	"We baked some cookies that you have to accept, if you want to enjoy this website. It simply doesn't work without. In order to gather information and make improvements, we should use some third-party cookies too. Can we? ";

const text =
	"Lorem ipsum dolor sit amet consectetur adipisicing elit. Veniam, quas accusantium deleniti aliquid et recusandae dignissimos non. Delectus, nam enim placeat impedit obcaecati magnam eum. Pariatur placeat culpa nesciunt provident vitae, aperiam velit. Odio eius aperiam voluptate molestias ex impedit mollitia architecto amet incidunt id, voluptatum voluptates deserunt, minus repellat. Lorem ipsum dolor sit amet consectetur adipisicing elit. Veniam, quas accusantium deleniti aliquid et recusandae dignissimos non. Delectus, nam enim placeat impedit obcaecati magnam eum. Pariatur placeat culpa nesciunt provident vitae, aperiam velit. Odio eius aperiam voluptate molestias ex impedit mollitia architecto amet incidunt id, voluptatum voluptates deserunt, minus repellat. Lorem ipsum dolor sit amet consectetur adipisicing elit. Veniam, quas accusantium deleniti aliquid et recusandae dignissimos non. Delectus, nam enim placeat impedit obcaecati magnam eum. Pariatur placeat culpa nesciunt provident vitae, aperiam velit. Odio eius aperiam voluptate molestias ex impedit mollitia architecto amet incidunt id, voluptatum voluptates deserunt, minus repellat. ";
</script>

<template>
	<div class="bg-slate-500 w-screen">
		<Cookie
			@buttonClick="clickHandler"
			:settings="cookieSettings"
			title="Welcome"
			:description="desc"
			:policyText="text"
			:rejectButtonVisibility="true"
		/>
	</div>
</template>

<style lang="postcss" scoped></style>
