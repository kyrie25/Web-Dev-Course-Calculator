<script setup>
import { CALCULATOR_KEYS, BUTTON_CATEGORIES, KEY_GROUPS } from "../constants/keys.js";

const emit = defineEmits(["press"]);
const props = defineProps({
	isDark: Boolean,
	pressedKey: String,
});

const memoryKeys = [
	CALCULATOR_KEYS.MEMORY_CLEAR,
	CALCULATOR_KEYS.MEMORY_RECALL,
	CALCULATOR_KEYS.MEMORY_ADD,
	CALCULATOR_KEYS.MEMORY_SUBTRACT,
	CALCULATOR_KEYS.MEMORY_STORE,
];

const gridKeys = [
	[CALCULATOR_KEYS.PERCENT, CALCULATOR_KEYS.CLEAR_ENTRY, CALCULATOR_KEYS.CLEAR_ALL, CALCULATOR_KEYS.BACKSPACE],
	[CALCULATOR_KEYS.RECIPROCAL, CALCULATOR_KEYS.SQUARE, CALCULATOR_KEYS.SQUARE_ROOT, CALCULATOR_KEYS.DIVIDE],
	[CALCULATOR_KEYS.SEVEN, CALCULATOR_KEYS.EIGHT, CALCULATOR_KEYS.NINE, CALCULATOR_KEYS.MULTIPLY],
	[CALCULATOR_KEYS.FOUR, CALCULATOR_KEYS.FIVE, CALCULATOR_KEYS.SIX, CALCULATOR_KEYS.SUBTRACT],
	[CALCULATOR_KEYS.ONE, CALCULATOR_KEYS.TWO, CALCULATOR_KEYS.THREE, CALCULATOR_KEYS.ADD],
	[CALCULATOR_KEYS.TOGGLE_SIGN, CALCULATOR_KEYS.ZERO, CALCULATOR_KEYS.DECIMAL, CALCULATOR_KEYS.EQUALS],
];

function onClick(k) {
	emit("press", k);
}

function getButtonClass(key) {
	const classes = ["key"];

	if (KEY_GROUPS.OPERATORS.includes(key)) classes.push(BUTTON_CATEGORIES.OPERATOR);
	if (KEY_GROUPS.MEMORY.includes(key)) classes.push(BUTTON_CATEGORIES.MEMORY);
	if (KEY_GROUPS.FUNCTIONS.includes(key)) classes.push(BUTTON_CATEGORIES.FUNCTION);
	if (key === CALCULATOR_KEYS.EQUALS) classes.push(BUTTON_CATEGORIES.EQUALS);
	if (props.pressedKey === key) classes.push("pressed");

	return classes;
}
</script>

<template>
	<div class="keypad-container" :class="{ dark: props.isDark }">
		<div class="memory-row">
			<button
				v-for="key in memoryKeys"
				:key="key"
				:class="getButtonClass(key)"
				@click="onClick(key)"
				:disabled="key === CALCULATOR_KEYS.MEMORY_DROPDOWN"
			>
				{{ key }}
			</button>
		</div>

		<div class="calc-grid">
			<template v-for="(keyRow, row) in gridKeys" :key="row">
				<button v-for="key in keyRow" :key="key" :class="getButtonClass(key)" @click="onClick(key)">
					{{ key }}
				</button>
			</template>
		</div>
	</div>
</template>

<style scoped>
.keypad-container {
	padding: 4px 8px 8px;
	background: transparent;
}

.memory-row {
	display: grid;
	grid-template-columns: repeat(5, 1fr);
	gap: 4px;
	margin-bottom: 4px;
}

.calc-grid {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	gap: 4px;
}

.key {
	height: 52px;
	border-radius: 4px;
	background: #f3f3f3;
	color: #000000;
	border: 1px solid rgba(0, 0, 0, 0.06);
	display: flex;
	align-items: center;
	justify-content: center;
	font-family: "Segoe UI", "Segoe UI Web", "Segoe UI Symbol", -apple-system, BlinkMacSystemFont, sans-serif;
	font-size: 14px;
	font-weight: 400;
	cursor: pointer;
	user-select: none;
	transition: all 0.1s ease;
}

.key:hover {
	background: #e6e6e6;
	border-color: rgba(0, 0, 0, 0.1);
}

.key:active,
.key.pressed {
	background: #d9d9d9;
	border-color: rgba(0, 0, 0, 0.12);
	transform: scale(0.98);
}

.key:focus {
	outline: 2px solid #005a9e;
	outline-offset: -2px;
}

.key:focus:not(:focus-visible) {
	outline: none;
}

/* Dark mode overrides */
.keypad-container.dark .key {
	background: #3a3a3a;
	color: #ffffff;
	border: 1px solid rgba(255, 255, 255, 0.06);
}

.keypad-container.dark .key:hover {
	background: #464646;
	border-color: rgba(255, 255, 255, 0.1);
}

.keypad-container.dark .key:active,
.keypad-container.dark .key.pressed {
	background: #525252;
	border-color: rgba(255, 255, 255, 0.12);
}

.keypad-container.dark .key:focus {
	outline: 2px solid #60a5fa;
	outline-offset: -2px;
}

/* Operator buttons */
.key.operator {
	background: #005a9e;
	color: white;
	border-color: #005a9e;
	font-weight: 500;
}

.key.operator:hover {
	background: #106ebe;
	border-color: #106ebe;
}

.key.operator:active,
.key.operator.pressed {
	background: #004578;
	border-color: #004578;
}

/* Memory buttons */
.key.memory {
	font-size: 12px;
	background: #f9f9f9;
	border-color: rgba(0, 0, 0, 0.04);
	font-weight: 500;
}

.keypad-container.dark .key.memory {
	background: #2d2d2d;
	border-color: rgba(255, 255, 255, 0.04);
}

.key.memory:hover {
	background: #ececec;
}

.keypad-container.dark .key.memory:hover {
	background: #393939;
}

/* Function buttons */
.key.function {
	background: #e6e6e6;
	border-color: rgba(0, 0, 0, 0.08);
	font-weight: 500;
}

.keypad-container.dark .key.function {
	background: #464646;
	border-color: rgba(255, 255, 255, 0.08);
}

.key.function:hover {
	background: #d9d9d9;
}

.keypad-container.dark .key.function:hover {
	background: #525252;
}

/* Equals button */
.key.equals {
	background: #005a9e;
	color: white;
	border-color: #005a9e;
	font-weight: 600;
	font-size: 16px;
}

.key.equals:hover {
	background: #106ebe;
	border-color: #106ebe;
}

.key.equals:active,
.key.equals.pressed {
	background: #004578;
	border-color: #004578;
}

/* Number keys get slightly different styling */
.key:not(.operator):not(.function):not(.memory):not(.equals) {
	background: #ffffff;
	border-color: rgba(0, 0, 0, 0.08);
}

.keypad-container.dark .key:not(.operator):not(.function):not(.memory):not(.equals) {
	background: #323232;
	border-color: rgba(255, 255, 255, 0.08);
}

.key:not(.operator):not(.function):not(.memory):not(.equals):hover {
	background: #f3f3f3;
}

.keypad-container.dark .key:not(.operator):not(.function):not(.memory):not(.equals):hover {
	background: #3e3e3e;
}

/* Disabled state */
.key:disabled {
	opacity: 0.5;
	cursor: not-allowed;
}

.key:disabled:hover {
	background: #f3f3f3;
	border-color: rgba(0, 0, 0, 0.06);
	transform: none;
}

.keypad-container.dark .key:disabled:hover {
	background: #3a3a3a;
	border-color: rgba(255, 255, 255, 0.06);
}
</style>
