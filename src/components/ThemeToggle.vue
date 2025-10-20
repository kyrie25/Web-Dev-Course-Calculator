<template>
	<button @click="$emit('toggle')" class="theme-toggle" :class="{ dark: isDark }">
		<svg
			v-if="isDark"
			width="16"
			height="16"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2"
			stroke-linecap="round"
			stroke-linejoin="round"
		>
			<circle cx="12" cy="12" r="5" />
			<path d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42" />
		</svg>
		<svg
			v-else
			width="16"
			height="16"
			viewBox="0 0 24 24"
			fill="none"
			stroke="currentColor"
			stroke-width="2"
			stroke-linecap="round"
			stroke-linejoin="round"
		>
			<path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z" />
		</svg>
	</button>
</template>

<script setup>
defineProps({
	isDark: Boolean,
});

defineEmits(["toggle"]);
</script>

<style scoped>
.theme-toggle {
	background: transparent;
	border: none;
	border-radius: 4px;
	width: 32px;
	height: 32px;
	display: flex;
	align-items: center;
	justify-content: center;
	cursor: pointer;
	transition: all 0.1s ease;
	color: #000;
}

.theme-toggle:hover {
	background: rgba(0, 0, 0, 0.06);
}

.theme-toggle:active {
	background: rgba(0, 0, 0, 0.1);
	transform: scale(0.96);
}

.theme-toggle.dark {
	color: #fff;
}

.theme-toggle.dark:hover {
	background: rgba(255, 255, 255, 0.06);
}

.theme-toggle.dark:active {
	background: rgba(255, 255, 255, 0.1);
}
</style>
