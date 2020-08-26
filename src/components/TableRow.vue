<template>
	<tr>
		<td>{{ user.id }}</td>
		<td>{{ user.name }}</td>
		<td>{{ user.date }}</td>
		<td>{{ user.email }}</td>
		<td>{{ user.phone }}</td>
		<td>{{ user.distance }} км</td>
		<td>{{ user.payment }}</td>
	</tr>
</template>

<script>
	export default {
		props: ['user']
	}	
</script>