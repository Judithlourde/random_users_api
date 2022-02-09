<template>
	<!-- <div>Home view</div> -->

	<h1>{{ title }}</h1>
	<div class="users">
		<h3>{{ name }}</h3>
		<img :src="image" alt="">
		<button v-on:click="fetchNew">Get New User</button>
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
	h1 {
		text-align: center;
	}

	button {
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

	h3 {
		margin-bottom: 10px;
	}

	img {
		margin-bottom: 15px;
		width: 100px;
		border-radius: 100%;
	}

	ul {
		text-align: center;
	}

	ul li {
		text-align: center;
		list-style: none;
	}
</style>
