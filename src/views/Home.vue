<template>
	<h1 class="title">{{ title }}</h1>

	<div class="users">
		<h3 class="user-name">{{ name }}</h3>
		<img class="user-image" :src="image" alt="">
		<button class="get-user" @click="fetchNew">Get New User</button>
	</div>

	<ul class="address"> 
		<h3>Address:</h3>
		<li>{{street.number}} {{ street.name }}</li>
		<li>{{ address.city }}</li>
		<li>{{ address.country }}</li>
	</ul>
	
</template>

<script>
	export default {
		name: 'home',
		data() {
			return {
				title: 'Users',
				name: '',
				email: '',
				image: '',
				street: '',
				address: '',
			}
		},
		
		created() {
			this.fetchNew();
			// const  result  = await res.json();
			// console.log(result.result[0]);
			// this.title = 'New Users';
		},

		mounted() {
			// this.title = 'New Users2';

		},

		methods: {
			async fetchNew() {
				const url = 'https://randomuser.me/api';
				const res = await fetch(url);
				const { results } = await res.json();
				console.log(results);
				this.name = `${results[0].name.first} ${results[0].name.last}`;
				this.image = results[0].picture.large;
				this.address = results[0].location;
				this.street = results[0].location.street;
			}
		}
	}
</script>

<style>
	.title {
		text-align: center;
	}

	.get-user {
		padding: 10px;
		background-color: rgb(202, 215, 186);	
		border-radius: 15px;
		margin-bottom: 20px;		
	}

	.users {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.user-name {
		margin-bottom: 10px;
	}

	.user-image {
		margin-bottom: 15px;
		width: 200px;
		border: 1px solid #eee;
		border-radius: 100%;
	}

	.address {
		text-align: center;
	}

	.address li {
		text-align: center;
		list-style: none;
	}
</style>
