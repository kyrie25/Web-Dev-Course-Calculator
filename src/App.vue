<script setup>
import Calculator from "./components/Calculator.vue";
</script>

<template>
	<div id="app" class="app-container">
		<div class="calculator-window">
			<Calculator />
		</div>
	</div>
</template>

<style>
.app-container {
	min-height: 100vh;
	display: flex;
	align-items: center;
	justify-content: center;
	padding: 20px;
	background: #f3f3f3;
	transition: all 0.3s ease;
	font-family: "Segoe UI", "Segoe UI Web", "Segoe UI Symbol", -apple-system, BlinkMacSystemFont, "Helvetica Neue", sans-serif;
}

.dark .app-container {
	background: #202020;
}

.calculator-window {
	width: 320px;
	background: #f9f9f9;
	border-radius: 8px;
	box-shadow: 0 8px 16px rgba(0, 0, 0, 0.14), 0 0 0 1px rgba(0, 0, 0, 0.05);
	overflow: hidden;
	transition: all 0.3s ease;
	border: none;
}

.dark .calculator-window {
	background: #2d2d2d;
	box-shadow: 0 8px 16px rgba(0, 0, 0, 0.4), 0 0 0 1px rgba(255, 255, 255, 0.08);
}

.calc-header {
	display: flex;
	align-items: center;
	justify-content: space-between;
	padding: 16px 20px 8px;
	border-bottom: none;
}

.calc-title {
	font-size: 20px;
	font-weight: 600;
	color: #000;
	margin: 0;
	font-family: "Segoe UI", "Segoe UI Web", "Segoe UI Symbol", -apple-system, BlinkMacSystemFont, sans-serif;
}

.dark .calc-title {
	color: #fff;
}
</style>
