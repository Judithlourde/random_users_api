<template>
	<h1 class="title">{{ title }}</h1>

	<div class="users">
		<h3 class="user-name">{{ firstName }}</h3>
		<h3 class="user-name">{{ lastName }}</h3>
		<img class="user-image" :src="image" alt="user-image">
		<button class="get-user" @click="fetchData">Get New User</button>
		<p v-if="error" class="error">{{ error }}</p>
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
				firstName: '',
				lastName: '',
				email: '',
				image: '',
				street: '',
				address: '',
				error: '',
			}
		},
		
		created: function() {
			// this.fetchNew();
			this.fetchData();
			// const  result  = await res.json();
			// console.log(result.result[0]);
			// this.title = 'New Users';
		},

		mounted() {
			// this.title = 'New Users2';
			//this.$store.dispatch("setCurrentUser");

		},

		methods: {
			// async fetchNew() {
			// 	const url = 'https://randomuser.me/api';
			// 	const res = await fetch(url);
			// 	const { results } = await res.json();
			// 	console.log(results);
			// 	this.name = `${results[0].name.first} ${results[0].name.last}`;
			// 	this.image = results[0].picture.large;
			// 	this.address = results[0].location;
			// 	this.street = results[0].location.street;
			// },

			async fetchData() {
                const url = 'https://randomuser.me/api/';
                const response = await fetch(url);
				try {
					await this.handleResponse(response);
				} catch (error) {
					console.log(error);
					this.error = error.message;
					// console.log(error.message);
					// console.log(error.name);

				}
                
            },

            async handleResponse(response) {
                console.log(response);
                if(response.status >= 200 && response.status < 300) {
                    console.log('ok');
                    const { results } = await response.json();
                    this.firstName = results[0].name.first;
                    this.lastName = results[0].name.last;
                    this.image = results[0].picture.large;
					return true;

                } else {
					console.log('feil');
					if(response.status === 404) {
						console.log('url ikke funnet');
						throw new Error('Url ikke funnet!');
					}
					if(response.status === 401) {
						console.log('ikke authorisert');
						throw new Error('ikke authorisert');
					}
					if(response.status > 500) {
						console.log('server error');
						throw new Error('Servor error!');
					}
					console.log('')
					throw new Error('Noe gikk galt!');
				}
            },
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
