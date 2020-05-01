<template>
    <div>
        <label for="">Email:</label><input type="text" v-model="email"> <br>
        <label for="">Password:</label><input type="password" v-model="password"> <br>
        <button @click="login">Login</button>
    </div>
</template>

<script>

import axios from 'axios';

export default {
    name: 'Login',
    data(){
        return {
            name: '',
            email: '',
            password: ''
        }
    },
    methods: {
        login() {
            let user = {
                email: this.email,
                password: this.password
            }
            axios.post('http://localhost:5000/login', user)
            .then(res => {
                if (res.status === 200) { // if success
                    localStorage.setItem('token', res.data.token);
                    this.$router.push('/');
                }
            }, err => {
                console.log(err.response);
                this.error = err.response.data.error;
                ;
                
            })
        }
    }
}
</script>

<style>
    input {
        display: block;
    }
</style>