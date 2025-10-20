<script setup>
import { Decimal } from "decimal.js";
import { ref, onMounted, onUnmounted } from "vue";
import Display from "./Display.vue";
import Keypad from "./Keypad.vue";
import ThemeToggle from "./ThemeToggle.vue";
import KeyboardHelp from "./KeyboardHelp.vue";
import { CALCULATOR_KEYS, KEYBOARD_MAPPINGS, KEY_GROUPS } from "../constants/keys.js";

const preferDark = window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches;

const display = ref("0");
const history = ref("");
const isDark = ref(preferDark);
const pressedKey = ref(null);
let waitingForOperand = false;

onMounted(() => {
	document.documentElement.classList.add("dark");
	document.addEventListener("keydown", handleKeyDown);
	document.addEventListener("keyup", handleKeyUp);
});

onUnmounted(() => {
	document.removeEventListener("keydown", handleKeyDown);
	document.removeEventListener("keyup", handleKeyUp);
});

let operator = null;
let operand = null;
let memory = Decimal(0);

function inputDigit(d) {
	if (waitingForOperand) {
		display.value = d;
		waitingForOperand = false;
		return;
	}
	if (display.value === "0" || display.value === "Error") display.value = d;
	else display.value += d;
}

function inputDot() {
	if (waitingForOperand) {
		display.value = "0.";
		waitingForOperand = false;
		return;
	}
	if (!display.value.includes(".")) display.value += ".";
}

function clearAll() {
	display.value = "0";
	history.value = "";
	operator = null;
	operand = null;
	waitingForOperand = false;
}

function clearEntry() {
	display.value = "0";
}

function backspace() {
	if (display.value === "0" || display.value === "Error") return;
	if (display.value.length === 1 || (display.value.length === 2 && display.value.startsWith("-"))) {
		display.value = "0";
	} else {
		display.value = display.value.slice(0, -1);
	}
}

function toggleSign() {
	if (display.value === "0" || display.value === "Error") return;
	if (display.value.startsWith("-")) display.value = display.value.slice(1);
	else display.value = "-" + display.value;
}

function percent() {
	const val = Decimal(display.value);
	if (isNaN(val)) return;
	display.value = val.div(100).toString();
	history.value = `${val}%`;
	waitingForOperand = true;
}

function square() {
	const val = Decimal(display.value);
	if (isNaN(val)) return;
	display.value = val.times(val).toString();
	history.value = `${val}²`;
	waitingForOperand = true;
}

function squareRoot() {
	const val = Decimal(display.value);
	if (isNaN(val) || val < 0) {
		display.value = "Error";
		return;
	}
	display.value = val.sqrt().toString();
	history.value = `√${val}`;
	waitingForOperand = true;
}

function reciprocal() {
	const val = Decimal(display.value);
	if (isNaN(val) || val === 0) {
		display.value = "Error";
		return;
	}
	display.value = Decimal(1).div(val).toString();
	history.value = `1/(${val})`;
	waitingForOperand = true;
}

function performOperation(nextOperator) {
	const inputValue = Decimal(display.value);
	if (isNaN(inputValue)) return;

	if (operand == null) {
		operand = inputValue;
	} else if (operator) {
		const result = calculate(operand, inputValue, operator);
		if (result === "Error") {
			display.value = "Error";
			return;
		}
		display.value = String(result);
		operand = result;
	}
	operator = nextOperator;
	waitingForOperand = true;
	history.value = operand + " " + (operator || "");
}

function calculate(a, b, op) {
	switch (op) {
		case CALCULATOR_KEYS.ADD:
			return Decimal(a).plus(Decimal(b)).toNumber();
		case CALCULATOR_KEYS.SUBTRACT:
			return Decimal(a).minus(Decimal(b)).toNumber();
		case CALCULATOR_KEYS.MULTIPLY:
			return Decimal(a).times(Decimal(b)).toNumber();
		case CALCULATOR_KEYS.DIVIDE:
			return b === 0 ? "Error" : Decimal(a).div(Decimal(b)).toNumber();
		default:
			return b;
	}
}

function equals() {
	const inputValue = Decimal(display.value);
	if (isNaN(inputValue)) return;

	if (operator && operand != null) {
		const result = calculate(operand, inputValue, operator);
		display.value = String(result);
		history.value += ` ${inputValue} =`;
		operator = null;
		operand = null;
		waitingForOperand = true;
	}
}

// Memory functions
function memoryClear() {
	memory = 0;
}

function memoryRecall() {
	display.value = Decimal(memory).toString();
	waitingForOperand = true;
}

function memoryAdd() {
	const val = Decimal(display.value);
	if (!isNaN(val)) memory = Decimal(memory).plus(val).toNumber();
}

function memorySubtract() {
	const val = Decimal(display.value);
	if (!isNaN(val)) memory = Decimal(memory).minus(val).toNumber();
}

function memoryStore() {
	const val = Decimal(display.value);
	if (!isNaN(val)) memory = val;
}

function toggleTheme() {
	isDark.value = !isDark.value;
	document.documentElement.classList.toggle("dark", isDark.value);
}

function handleKey(key) {
	if (/^\d$/.test(key)) inputDigit(key);
	else if (key === CALCULATOR_KEYS.DECIMAL) inputDot();
	else if (key === CALCULATOR_KEYS.CLEAR_ALL) clearAll();
	else if (key === CALCULATOR_KEYS.CLEAR_ENTRY) clearEntry();
	else if (key === CALCULATOR_KEYS.BACKSPACE) backspace();
	else if (key === CALCULATOR_KEYS.TOGGLE_SIGN) toggleSign();
	else if (key === CALCULATOR_KEYS.PERCENT) percent();
	else if (key === CALCULATOR_KEYS.SQUARE) square();
	else if (key === CALCULATOR_KEYS.SQUARE_ROOT) squareRoot();
	else if (key === CALCULATOR_KEYS.RECIPROCAL) reciprocal();
	else if (KEY_GROUPS.OPERATORS.slice(1).includes(key)) performOperation(key);
	else if (key === CALCULATOR_KEYS.EQUALS) equals();
	else if (key === CALCULATOR_KEYS.MEMORY_CLEAR) memoryClear();
	else if (key === CALCULATOR_KEYS.MEMORY_RECALL) memoryRecall();
	else if (key === CALCULATOR_KEYS.MEMORY_ADD) memoryAdd();
	else if (key === CALCULATOR_KEYS.MEMORY_SUBTRACT) memorySubtract();
	else if (key === CALCULATOR_KEYS.MEMORY_STORE) memoryStore();
}

function handleKeyDown(event) {
	if (event.ctrlKey || event.altKey || event.metaKey) return;

	const key = event.key;
	let calculatorKey = null;

	// Map keyboard keys to calculator keys
	if (/^[0-9]$/.test(key)) {
		calculatorKey = key;
	} else if (KEYBOARD_MAPPINGS[key]) {
		calculatorKey = KEYBOARD_MAPPINGS[key];
	} else if (key.toLowerCase() === "c") {
		calculatorKey = CALCULATOR_KEYS.CLEAR_ALL;
	}

	if (calculatorKey) {
		event.preventDefault();
		pressedKey.value = calculatorKey;
		handleKey(calculatorKey);
	}
}

function handleKeyUp() {
	setTimeout(() => {
		pressedKey.value = null;
	}, 100);
}
</script>

<template>
	<div>
		<div class="calc-header">
			<h2 class="calc-title">Calculator</h2>
			<div class="header-actions">
				<KeyboardHelp :isDark="isDark" />
				<ThemeToggle :isDark="isDark" @toggle="toggleTheme" />
			</div>
		</div>
		<Display :value="display" :history="history" :isDark="isDark" />
		<Keypad @press="handleKey" :isDark="isDark" :pressedKey="pressedKey" />
	</div>
</template>

<style scoped>
.header-actions {
	display: flex;
	align-items: center;
	gap: 4px;
}
</style>
