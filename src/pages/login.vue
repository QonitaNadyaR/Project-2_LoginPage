<script setup lang="ts">
import { useAuthStore } from '@/stores/auth';
import { ref } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';


const auth = useAuthStore()
const username = ref('')
const password = ref('')
const router = useRouter()

const onLogin = async () => {
    if (username.value === "" || password.value === "") {
        alert("Username or Password can't be empty")
    } else {
        try {
            const response = await axios.post('http://localhost:3000/login', {
                username: username.value,
                password: password.value,
            })

            auth.login(username.value, password.value)
            console.log(response);
        } catch (error) {
            console.error('Login error:', error);
        }
    }
}
// auth.login(username.value)
// router.push('/')

</script>

<template>
    <div>
        <h1>Login Page</h1>
        <div class="flex flex-col gap-2">
            <input type="text" v-model="username" class="border p-2" placeholder="Username" />
            <input type="text" v-model="password" class="border p-2" placeholder="Password" />
            <button @click="onLogin()" class="bg-blue-500 text-white py-1 px-3">Login</button>
        </div>
    </div>
</template>