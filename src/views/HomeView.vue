<template>
	<v-container class="mb-lg-5">
		<v-row>
			<!-- Левая колонка - Изображения товара -->
			<v-col cols="12" md="6">
				<slider>2</slider>
			</v-col>

			<!-- Правая колонка - Описание товара -->
			<v-col cols="12" md="6" class="justify-space-between d-flex flex-column">
				<h2 class="text-h6 text-lg-h4 font-weight-bold mb-2">
					{{ product.title }}
				</h2>
				<p class="text-h5 font-weight-bold mb-4 text-primary">
					{{ product.price }} ₽
				</p>

				<!-- Размеры -->
				<v-select
					label="Выберите размер"
					:items="product.sizes"
					density="compact"
					v-model="selectedSize"
					outlined
				/>
				<!-- Color -->
				<selectColor></selectColor>
				<!-- Кнопка "Купить" -->
				<v-dialog max-width="500">
					<template v-slot:activator="{ props: activatorProps }">
						<v-btn
							min-width="3  00"
							color="primary"
							block
							class="mt-4"
							v-bind="activatorProps"
						>
							Купить
						</v-btn>
					</template>

					<template v-slot:default="{ isActive }">
						<dialogForm></dialogForm>
					</template>
				</v-dialog>
			</v-col>
		</v-row>
		<v-row>
			<v-col cols="12">
				<v-tabs v-model="tab" class="mt-6">
					<v-tab value="description" @click.prevent="tab = 'description'">
						Описание
					</v-tab>
					<v-tab value="specs" @click.prevent="tab = 'specs'">
						Характеристики
					</v-tab>
				</v-tabs></v-col
			>
			<v-col cols="12">
				<v-window v-model="tab" class="tabsWindows" style="overflow: hidden">
					<v-window-item value="description">
						<p class="mt-4">{{ product.description }}</p>
					</v-window-item>

					<v-window-item value="specs">
						<v-table class="mt-4 mb-4">
							<tbody>
								<tr v-for="(value, key) in product.specs" :key="key">
									<td class="font-weight-bold">{{ key }}</td>
									<td>{{ value }}</td>
								</tr>
							</tbody>
						</v-table>
					</v-window-item>
				</v-window></v-col
			>
		</v-row>
	</v-container>
</template>

<script setup>
import { ref } from "vue";
import slider from "@/components/slider.vue";
import dialogForm from "@/components/dialogForm.vue";
import selectColor from "@/components/selectColor.vue";
// Пример данных товара
const product = ref({
	title: "Полуботинки женские 423",
	price: 1392.99,
	images: [
		"https://www.marko.by/image/cache/catalog/products/marko/marko-423/1-800x800.jpg",
		"https://www.marko.by/image/cache/catalog/products/marko/marko-423/2-800x800.jpg",
		"https://www.marko.by/image/cache/catalog/products/marko/marko-423/3-800x800.jpg"
	],
	sizes: ["36", "37", "38", "39", "40"],
	description:
		"В мире моды и удобства обуви женские кроссовки давно заняли уверенную позицию. Они стали не только частью спортивного гардероба, но и важным элементом повседневного стиля. Данная модель кроссовок — это идеальный выбор для девушек, которые ценят комфорт, стиль и универсальность. Современный дизайн, легкость и практичность делают их незаменимыми в любой ситуации: будь то прогулка по городу, встреча с друзьями или активный день на ногах Дизайн и стиль Эта модель кроссовок сочетает в себе минималистичный и стильный дизайн, подходящий под большинство современных трендов. Бело-серая цветовая гамма — это классика, которая никогда не выходит из моды. Особенности дизайна: ✔ Лаконичные линии и плавные изгибы делают модель универсальной для любого образа.✔ Контрастные вставки придают элегантность и легкость.✔ Перфорация в области носка не только служит декоративным элементом, но и улучшает вентиляцию.✔ Высокая подошва добавляет немного роста, но при этом остается удобной для длительной носки.✔ Комбинированные материалы верха создают эффектный внешний вид.Эти кроссовки можно легко сочетать с джинсами, спортивными костюмами, платьями и даже деловыми брюками, создавая овременный casual-образ.",
	specs: {
		"Материал верха": "Натуральная кожа",
		"Материал подкладки": "Текстиль",
		"Подошва": "Полиуретан",
		"Цвет": "Черный"
	}
});

const selectedSize = ref(null);
const tab = ref("description");
</script>
<style lang="scss">
.tabsWindows {
	height: 300px;
	@media (max-width: 1024px) {
		height: auto;
	}
}
</style>
