<template>
	<v-row>
		<v-col cols="12" md="6">
			<h3 class="text-h6 text-center mb-4">Выберите цвет товара</h3>
			<v-row>
				<v-col
					v-for="(color, index) in colors"
					:key="index"
					cols="2"
					class="pa-4"
				>
					<div class="color-item">
						<v-btn
							:color="color.value"
							class="color-btn"
							icon
							:class="{ selected: selectedColor === color.value }"
							@click="selectColor(color.value)"
						>
							<v-icon v-if="selectedColor === color.value" color="white"
								>mdi-check</v-icon
							>
						</v-btn>
					</div>
				</v-col>
			</v-row>
			<v-card class="selected-color-card mt-6" outlined>
				<v-card-text class="text-center pa-2">
					<span class="font-weight-medium">Выбранный цвет: </span>
					<span :style="{ color: selectedColor }">{{ selectedColorName }}</span>
				</v-card-text>
			</v-card>
		</v-col>
	</v-row>
</template>

<script setup>
import { ref, computed } from "vue";

const colors = ref([
	{ name: "Белый", value: "#ffffff" },
	{ name: "Черный", value: "#000000" },
	{ name: "Серый", value: "#b0b0b0" },
	{ name: "Красный", value: "#ff3b30" },
	{ name: "Синий", value: "#007aff" },
	{ name: "Зеленый", value: "#34c759" }
]);

const selectedColor = ref(colors.value[0].value);

const selectedColorName = computed(() => {
	return (
		colors.value.find((color) => color.value === selectedColor.value)?.name ||
		"Не выбран"
	);
});

const selectColor = (color) => {
	selectedColor.value = color;
};
</script>

<style scoped>
.color-item {
	position: relative;
	display: flex;
	width: 40px;
}
.color-selector {
	max-width: 200px;
	margin: auto;
}

.color-btn {
	width: 40px;
	height: 40px;
	display: block;
	border-radius: 50%;
	transition: 0.3s;
	border: 2px solid transparent;
}

.color-btn.selected {
	border-color: #33333342;
}
</style>
