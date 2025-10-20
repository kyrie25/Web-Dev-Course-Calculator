<!-- Generated using Github Copilot -->
<template>
	<div class="help-container">
		<button @click="toggleHelp" class="help-button" :class="{ dark: isDark }">
			<svg
				width="16"
				height="16"
				viewBox="0 0 24 24"
				fill="none"
				stroke="currentColor"
				stroke-width="2"
				stroke-linecap="round"
				stroke-linejoin="round"
			>
				<circle cx="12" cy="12" r="10" />
				<path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3" />
				<path d="M12 17h.01" />
			</svg>
		</button>

		<div v-if="showHelp" class="help-popup" :class="{ dark: isDark }">
			<div class="help-header">
				<h3>Keyboard Shortcuts</h3>
				<button @click="showHelp = false" class="close-button">×</button>
			</div>
			<div class="help-content">
				<div class="shortcut-group">
					<h4>Numbers & Operations</h4>
					<div class="shortcut"><kbd>0-9</kbd> Numbers</div>
					<div class="shortcut"><kbd>.</kbd> Decimal point</div>
					<div class="shortcut"><kbd>+ - * /</kbd> Basic operations</div>
					<div class="shortcut"><kbd>Enter</kbd> or <kbd>=</kbd> Calculate result</div>
				</div>
				<div class="shortcut-group">
					<h4>Functions</h4>
					<div class="shortcut"><kbd>%</kbd> Percentage ({{ CALCULATOR_KEYS.PERCENT }})</div>
					<div class="shortcut"><kbd>S</kbd> Square root ({{ CALCULATOR_KEYS.SQUARE_ROOT }})</div>
					<div class="shortcut"><kbd>Q</kbd> Square ({{ CALCULATOR_KEYS.SQUARE }})</div>
					<div class="shortcut"><kbd>R</kbd> Reciprocal ({{ CALCULATOR_KEYS.RECIPROCAL }})</div>
					<div class="shortcut"><kbd>F9</kbd> Change sign ({{ CALCULATOR_KEYS.TOGGLE_SIGN }})</div>
				</div>
				<div class="shortcut-group">
					<h4>Clear & Delete</h4>
					<div class="shortcut"><kbd>Backspace</kbd> Delete last digit ({{ CALCULATOR_KEYS.BACKSPACE }})</div>
					<div class="shortcut"><kbd>Delete</kbd> Clear entry ({{ CALCULATOR_KEYS.CLEAR_ENTRY }})</div>
					<div class="shortcut"><kbd>Esc</kbd> or <kbd>C</kbd> Clear all ({{ CALCULATOR_KEYS.CLEAR_ALL }})</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref } from "vue";
import { CALCULATOR_KEYS } from "../constants/keys.js";

defineProps({
	isDark: Boolean,
});

const showHelp = ref(false);

function toggleHelp() {
	showHelp.value = !showHelp.value;
}
</script>

<style scoped>
.help-container {
	position: relative;
}

.help-button {
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

.help-button:hover {
	background: rgba(0, 0, 0, 0.06);
}

.help-button:active {
	background: rgba(0, 0, 0, 0.1);
	transform: scale(0.96);
}

.help-button.dark {
	color: #fff;
}

.help-button.dark:hover {
	background: rgba(255, 255, 255, 0.06);
}

.help-button.dark:active {
	background: rgba(255, 255, 255, 0.1);
}

.help-popup {
	position: fixed;
	top: 60px;
	right: 20px;
	width: 300px;
	max-width: calc(100vw - 40px);
	background: #fff;
	border: 1px solid rgba(0, 0, 0, 0.1);
	border-radius: 8px;
	box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
	z-index: 1000;
	font-family: "Segoe UI", "Segoe UI Web", "Segoe UI Symbol", -apple-system, BlinkMacSystemFont, sans-serif;
}

.help-popup.dark {
	background: #2d2d2d;
	border-color: rgba(255, 255, 255, 0.1);
	box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
}

.help-header {
	display: flex;
	align-items: center;
	justify-content: space-between;
	padding: 16px;
	border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.help-popup.dark .help-header {
	border-bottom-color: rgba(255, 255, 255, 0.1);
}

.help-header h3 {
	margin: 0;
	font-size: 16px;
	font-weight: 600;
	color: #000;
}

.help-popup.dark .help-header h3 {
	color: #fff;
}

.close-button {
	background: none;
	border: none;
	font-size: 18px;
	cursor: pointer;
	padding: 4px;
	border-radius: 4px;
	color: #666;
}

.close-button:hover {
	background: rgba(0, 0, 0, 0.06);
}

.help-popup.dark .close-button {
	color: #ccc;
}

.help-popup.dark .close-button:hover {
	background: rgba(255, 255, 255, 0.06);
}

.help-content {
	padding: 16px;
	max-height: 400px;
	overflow-y: auto;
}

.shortcut-group {
	margin-bottom: 16px;
}

.shortcut-group:last-child {
	margin-bottom: 0;
}

.shortcut-group h4 {
	margin: 0 0 8px 0;
	font-size: 14px;
	font-weight: 600;
	color: #000;
}

.help-popup.dark .shortcut-group h4 {
	color: #fff;
}

.shortcut {
	display: flex;
	align-items: center;
	justify-content: space-between;
	padding: 4px 0;
	font-size: 13px;
	color: #666;
}

.help-popup.dark .shortcut {
	color: #ccc;
}

kbd {
	background: #f3f3f3;
	border: 1px solid #ccc;
	border-radius: 3px;
	padding: 2px 6px;
	font-size: 11px;
	font-family: monospace;
	color: #333;
}

.help-popup.dark kbd {
	background: #404040;
	border-color: #555;
	color: #ddd;
}
</style>
