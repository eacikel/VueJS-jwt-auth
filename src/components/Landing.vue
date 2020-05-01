<template>
    <div>
        <h1 style="color:green">HELLO {{ name }}</h1>
        <h6 style="color:red">YOUR EMAIL IS: {{ email }}</h6>
        <button @click="logout" style="color:white;background-color:black">Logout</button>
    </div>
</template>

<script>

import axios from 'axios';

export default {
    name: 'Landing',
    data() {
        return {
            name: '',
            email: '',
        }
    },
    created() {
        if (localStorage.getItem('token') === null) { //user is not authorized
            this.$router.push('/login');
        }
    },
    mounted() {
        axios.get('http://localhost:5000/user', { headers: { token: localStorage.getItem('token') } })
        .then(res => {
            this.name = res.data.user.name;
            this.email = res.data.user.email;
        })
    },
    methods: {
        logout() {
            localStorage.clear();
            this.$router.push('/login');
        }
    }
}
</script>