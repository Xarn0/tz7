<template>
	<v-container class="form-container">
		<v-card class="pa-5" elevation="10">
			<v-card-title class="text-sm-h5 text-center"
				>Закажите сейчас</v-card-title
			>
			<v-card-subtitle class="text-center mb-3 d-none d-md-block"
				>Заполните форму, и мы свяжемся с вами</v-card-subtitle
			>

			<v-form ref="form" class="dialogForm" v-model="valid">
				<v-text-field
					v-model="name"
					label="Ваше имя"
					variant="outlined"
					:rules="[rules.required]"
					prepend-icon="mdi-account"
					density="compact"
					hide-details
					single-line
				></v-text-field>

				<v-text-field
					v-model="phone"
					density="compact"
					label="Телефон"
					single-line
					variant="outlined"
					hide-details
					:rules="[rules.required, rules.phone]"
					prepend-icon="mdi-phone"
				></v-text-field>

				<v-btn color="primary" block :disabled="!valid" @click="submitForm">
					Заказать
				</v-btn>
			</v-form>
		</v-card>
	</v-container>
</template>

<script setup>
import { ref } from "vue";

const form = ref(null);
const valid = ref(false);
const name = ref("");
const phone = ref("");

const rules = {
	required: (value) => !!value || "Обязательное поле",

	phone: (value) =>
		/^\+?\d{10,15}$/.test(value) || "Некорректный номер телефона"
};

const submitForm = () => {
	if (form.value.validate()) {
		alert("Форма успешно отправлена!");
	}
};
</script>

<style scoped>
.form-container {
	max-width: 500px;
	margin: auto;
}
.dialogForm {
	display: flex;
	flex-direction: column;
	gap: 10px;
}
</style>
