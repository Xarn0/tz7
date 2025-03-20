<template>
	<v-container>
		<v-row>
			<!-- Левая колонка - Изображения товара -->
			<v-col cols="12" md="6">
				<v-carousel hide-delimiters>
					<v-carousel-item
						v-for="(image, index) in product.images"
						:key="index"
						:src="image"
						cover
					/>
				</v-carousel>
			</v-col>

			<!-- Правая колонка - Описание товара -->
			<v-col cols="12" md="6">
				<h2 class="text-h4 font-weight-bold">{{ product.title }}</h2>
				<p class="text-h5 font-weight-bold text-primary">
					{{ product.price }} ₽
				</p>

				<!-- Размеры -->
				<v-select
					label="Выберите размер"
					:items="product.sizes"
					v-model="selectedSize"
					outlined
				/>

				<!-- Кнопка "Купить" -->
				<v-btn color="primary" block class="mt-4" @click="buyProduct">
					Купить
				</v-btn>

				<!-- Табуляция "Описание" / "Характеристики" -->
				<v-tabs v-model="tab" class="mt-6">
					<v-tab value="description">Описание</v-tab>
					<v-tab value="specs">Характеристики</v-tab>
				</v-tabs>

				<v-window v-model="tab">
					<v-window-item value="description">
						<p class="mt-4">{{ product.description }}</p>
					</v-window-item>

					<v-window-item value="specs">
						<v-table class="mt-4">
							<tbody>
								<tr v-for="(value, key) in product.specs" :key="key">
									<td class="font-weight-bold">{{ key }}</td>
									<td>{{ value }}</td>
								</tr>
							</tbody>
						</v-table>
					</v-window-item>
				</v-window>
			</v-col>
		</v-row>
	</v-container>
</template>

<script setup>
import { ref } from "vue";

// Пример данных товара
const product = ref({
	title: "Полуботинки женские 423",
	price: 139.99,
	images: [
		"https://www.marko.by/image/cache/catalog/products/marko/marko-423/1-800x800.jpg",
		"https://www.marko.by/image/cache/catalog/products/marko/marko-423/2-800x800.jpg",
		"https://www.marko.by/image/cache/catalog/products/marko/marko-423/3-800x800.jpg"
	],
	sizes: ["36", "37", "38", "39", "40"],
	description:
		"Женские полуботинки Marko 423 — стильное и удобное решение для повседневной носки.",
	specs: {
		"Материал верха": "Натуральная кожа",
		"Материал подкладки": "Текстиль",
		"Подошва": "Полиуретан",
		"Цвет": "Черный"
	}
});

// Выбранный размер
const selectedSize = ref(null);
const tab = ref("description");

// Функция покупки
const buyProduct = () => {
	if (!selectedSize.value) {
		alert("Выберите размер перед покупкой!");
		return;
	}
	alert(
		`Товар "${product.value.title}" (${selectedSize.value} размер) добавлен в корзину!`
	);
};
</script>
