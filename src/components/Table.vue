<template>
	<div>
		<h5 class="title">Участники забега</h5>
		<!-- речь скорее о сортировки, не о фильтрации, будет исправлено в поставновке тестового. сейчас не выполнено -->

		<!-- <div class="form-group">
			<label for="filter">Фильтрация по:</label>
			<select id="filter" class="form-control" v-model="filter">
				<option v-for="option in options" :key="option" v-bind:value="option.value">{{ option.text }}</option>
			</select>
		</div> -->
		<div class="table">
			<tr>
				<th>#</th>
				<th>ФИО</th>
				<th>Дата рождения</th>
				<th>E-mail</th>
				<th>Телефон</th>
				<th>Дистанция</th>
				<th>Сумма взноса</th>
			</tr>
			<TableRow 
				v-for="user of users"
				:key="user"
				v-bind:user="user"
			/>
		</div>
	</div>
</template>

<script>
	import TableRow from '@/components/TableRow.vue'

	export default {
		props: ['users'],
		data() {
			return {
				filter: '',
				options: [
					{text: 'Дате регистрации', value: 'Дате регистрации'},
					{text: 'Сумме взноса', value: 'Сумме взноса'},
					{text: 'Дистанции забега', value: 'Дистанции забега'},
				]
			}
		},
		methods: {
			getFilterData() {
				console.log(this.filter)
			}
		},
		components: {
			TableRow
		}
	}
</script>