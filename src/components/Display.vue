<script setup>
import { toRef } from "vue";
const props = defineProps({
	value: [String, Number],
	history: String,
	isDark: Boolean,
});
const value = toRef(props, "value");
</script>

<template>
	<div class="display" :class="{ dark: props.isDark }">
		<div class="history" v-if="props.history">{{ props.history }}</div>
		<div class="value">{{ value }}</div>
	</div>
</template>

<style scoped>
.display {
	background: transparent;
	padding: 20px 20px 16px;
	min-height: 120px;
	display: flex;
	flex-direction: column;
	justify-content: flex-end;
	align-items: flex-end;
	text-align: right;
}

.history {
	font-size: 14px;
	color: rgba(0, 0, 0, 0.6);
	margin-bottom: 8px;
	font-family: "Segoe UI", "Segoe UI Web", "Segoe UI Symbol", sans-serif;
	font-weight: 400;
}

.display.dark .history {
	color: rgba(255, 255, 255, 0.6);
}

.value {
	font-size: 48px;
	font-weight: 600;
	line-height: 1;
	color: #000000;
	font-family: "Segoe UI", "Segoe UI Web", "Segoe UI Symbol", sans-serif;
	word-break: break-all;
	max-width: 100%;
	overflow: hidden;
	letter-spacing: -1px;
}

.display.dark .value {
	color: #ffffff;
}

/* Responsive font sizing */
@media (max-width: 400px) {
	.value {
		font-size: 36px;
	}
}
</style>
