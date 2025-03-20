<template>
	<div class="flex">
		<!-- Большой слайдер -->
		<swiper
			:slides-per-view="1"
			:modules="[Thumbs]"
			:thumbs="{ swiper: secondSwiper }"
			class="main-swiper"
		>
			<SwiperSlide class="swiper-slide-big" v-for="el in 4">
				<img :src="`@/assets/img/${el}.webp`" alt="" />
			</SwiperSlide>
		</swiper>

		<!-- Миниатюры -->
		<swiper
			:slides-per-view="4"
			:space-between="10"
			:modules="[Thumbs]"
			@swiper="setSecondSwiper"
			direction="vertical"
			class="thumbs-swiper"
		>
			<SwiperSlide class="swiper-slide-2" v-for="el in 4">
				<img :src="`/${el}.webp`" alt="" />
			</SwiperSlide>
		</swiper>
	</div>
</template>

<script setup>
import { ref } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Thumbs } from "swiper/modules";
import "swiper/css";

const secondSwiper = ref(null);

const setSecondSwiper = (swiper) => {
	secondSwiper.value = swiper;
};
</script>

<style>
.swiper-slide2 {
	width: 90px;
	/* max-height: 300px; */
	background: #0394;
	color: white;
	border: 1px solid transparent;
	cursor: pointer;
}
.swiper-slide2 img {
	max-width: 100%;
	object-fit: contain;
}
.swiper-slide2.swiper-slide-thumb-active {
	border: 1px solid orange;
}
.swiper-slide-big {
	/* width: 50%; */
	height: 400px;
	background: #0394;
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
	gap: 20px;
}
.thumbs-swiper {
	padding-right: 65px;
	padding-bottom: 4px;
	width: 190px;
	height: 400px;
}
</style>
