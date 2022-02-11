<template>
    <section class="">
        <h1 class="user2">{{ title }}</h1>

        <input type="text" v-model="nameValue">
        <span>{{ nameValue }}</span>
        <span>{{ personEmail }}</span>

        <ul class="">
            <li v-for="person in people" :key="person.id.value">
                {{ person.name.first }} {{ person.name.last }}
            </li>
        </ul>

        <button @click="fetchData" class="get-new-list">Get New List</button> <br>

        <button @click="findPerson">Get Email</button> <br>

        <button @click="onlyMale">Only Male</button>

        <button @click="sortAlpha">Sorting</button>
    </section>
</template>

<script>
    export default {
        data() {
            return {
                title: 'Users List',
                nameValue: '',
                people: [],
                personEmail: '',
            }  
        },

        created() {
            // console.log('started');
            this.fetchData();
            this.sumThis();
            
        },

        methods: {
            async fetchData() {
                const url = 'https://randomuser.me/api/?page=2&results=20';
                const res = await fetch(url);
                const { results } = await res.json()
                // console.log(results); 
                this.people = results;
                // console.log(this.people)
            },

            findPerson() {
                const person = this.people.find(user => {
                    return user.name.last === this.nameValue;
                });
                this.personEmail = person.email; 
            },

            onlyMale() {
                const genderList = this.people.filter(user => {
                    return user.gender === 'male';
                });
                this.people = genderList;
            },

            sortAlpha() {
                const sortedData = this.people.sort((a, b) => {
                    if(a.name.last > b.name.last) return 1;
                    if(a.name.last < b.name.last) return -1;
                    return 0;
                });
                this.people = sortedData;
            },

            sumThis() {
                const numbers = [1, 4, 6, 8];
                const sum = numbers.reduce((result, numb) => {
                    return numb + result;
                }, 0);
                console.log(sum);
            }
        }
    }
</script>

<style>
    .get-new-list, 
    button {
        padding: 20px;
    }

    input {
        padding: 20px;
        background-color: aquamarine;
    }

</style>