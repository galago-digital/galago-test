<template>
	<div>
		<h5 class="title">Заполните форму для участия в забеге</h5>
		<form v-on:submit.prevent="onSubmit" novalidate="true">
			<div class="form-group">
				<label for="name">ФИО</label>
				<input type="text" class="form-control" id="name" v-model="name">
			</div>
			<div class="form-group">
				<label for="date">Дата рождения</label>
				<input type="date" class="form-control" id="date" v-model="date">
			</div>
			<p class="error" v-if="errors.length">
				<span v-for="error in errors" :key="error">{{ error }}</span>
			</p>
			<div class="form-group">
				<label for="email">E-mail</label>
				<input type="email" class="form-control" id="email" v-model="email">
			</div>
			<div class="form-group">
				<label for="phone">Телефон</label>
				<masked-input type="phone" class="form-control" id="phone" v-model="phone" mask="\+\7 (111) 111-11-11"/>
			</div>
			<div class="form-group">
				<label for="distance">Дистанция(км)</label>
				<select id="distance" class="form-control" v-model="distance">
					<option>3</option>
					<option>5</option>
					<option>10</option>
				</select>
			</div>
			<div class="form-group">
				<label for="payment">Сумма взноса</label>
				<input type="text" class="form-control" id="payment" v-model="payment">
			</div>
			<button type="submit" class="btn btn-primary" :disabled="!name || !date || !email || !phone || !distance || !payment">Отправить заявку</button>
		</form>
	</div>
</template>

<script>
	import MaskedInput from 'vue-masked-input'

	export default {
		props: ['users'],
		data() {
			return {
				name: '',
				date: '',
				email: '',
				phone: '',
				distance: '',
				payment: '',
				errors: []
			}
		},
		methods: {
			onSubmit() {
				this.errors = [];

				if (!this.validEmail(this.email)) {
					this.errors.push('Укажите корректный адрес электронной почты.');
				} else {
					const newUser = {
						id: this.users.length + 1,
						name: this.name,
						date: this.date,
						email: this.email,
						phone: this.phone,
						distance: this.distance,
						payment: this.payment
					}

					this.$emit('add-user', newUser)
				}

				if (!this.errors.length) {
					return true;
				}
				// не очищаются поля формы после добавления пользователя
			},
			validEmail: function (email) {
				var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
					return re.test(email);
			}
		},
		components: {
			MaskedInput
		}
	}
</script>

<style scoped>
	.error {
		margin: 0;
		color: red;
		font-size: 12px;
	}
</style>










