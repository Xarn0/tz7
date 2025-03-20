<template>
	<div class="flex">
		<!-- Большой слайдер -->
		<swiper
			:slides-per-view="1"
			:modules="[Thumbs]"
			:thumbs="{ swiper: secondSwiper }"
			class="main-swiper ma-0"
		>
			<SwiperSlide class="swiper-slide-big" v-for="el in 4">
				<img :src="getImage(el)" alt="" />
			</SwiperSlide>
		</swiper>

		<!-- Миниатюры -->
		<swiper
			:slides-per-view="4"
			:space-between="10"
			:modules="[Thumbs]"
			@swiper="setSecondSwiper"
			class="thumbs-swiper"
			:breakpoints="{
				450: { direction: 'vertical', slidesPerView: 3 }, // Меньше 450px - вертикально
				0: { direction: 'horizontal', slidesPerView: 4 } // Больше 450px - горизонтально
			}"
		>
			<SwiperSlide class="swiper-slide-2" v-for="el in 4">
				<div class="swiper-slide-2-img">
					<img :src="getImage(el)" alt="" />
				</div>
			</SwiperSlide>
		</swiper>
	</div>
</template>

<script setup>
import { ref, computed, watch } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Thumbs } from "swiper/modules";
import "swiper/css";

const secondSwiper = ref(null);

const setSecondSwiper = (swiper) => {
	secondSwiper.value = swiper;
};

const images = Object.fromEntries(
	Object.entries(
		import.meta.glob("/src/assets/img/*.webp", { eager: true })
	).map(([path, module]) => [
		path.split("/").pop().replace(".webp", ""),
		module.default
	])
);

const getImage = (index) => images[index];
</script>

<style>
.swiper-slide-2 {
	width: 90px;
	max-height: 300px;
	color: white;
	border: 1px solid transparent;
	cursor: pointer;
	overflow: hidden;
}
.swiper-slide-2 img {
	width: 100%;
	object-fit: cover;
}
.swiper-slide-2-img {
	width: 90px;
}
.swiper-slide-2.swiper-slide-thumb-active {
	border: 1px solid orange;
}
.swiper-slide-big {
	/* width: 50%; */
	height: 400px;
	color: white;
	display: flex;
	align-items: center;
	justify-content: center;
	font-size: 24px;
}
.swiper-slide-big img {
	max-width: 100%;
	object-fit: cover;
}
.flex {
	display: flex;
	gap: 10px;
}
.thumbs-swiper {
	padding-right: 65px;
	padding-bottom: 4px;
	width: 190px;
	height: 400px;
}
@media (max-width: 450px) {
	.flex {
		flex-direction: column;
	}
	.swiper-slide-big {
		width: 100%;
	}
	.thumbs-swiper {
		width: 100%;
		padding-right: 0;
		padding-bottom: 0px;
		height: auto;
	}
}
</style>
