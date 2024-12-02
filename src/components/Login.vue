<template>
    <div class="login">
        <h1>Login</h1>
        <form @submit.prevent="handleLogin">
            <div class="form-group">
                <label for="email">Email</label>
                <input type="email" id="email" v-model="email" placeholder="Enter your email" required />
            </div>
            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" id="password" v-model="password" placeholder="Enter your password" required />
            </div>
            <button type="submit">Login</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'LoginPage',
    data() {
        return {
            email: '',
            password: ''
        };
    },
    methods: {
        handleLogin() {
            const users = JSON.parse(localStorage.getItem('users')) || [];
            const user = users.find(user => user.email === this.email && user.password === this.password);

            if (user) {
                alert(`Welcome back, ${user.name}!`);
                this.$router.push('/dashboard'); // Redirect to a dashboard or another page
            } else {
                alert('Invalid email or password. Please try again.');
            }
        }
    }
};
</script>

<style scoped>
.login {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background-color: #f9f9f9;
}

h1 {
    text-align: center;
    margin-bottom: 20px;
}

.form-group {
    margin-bottom: 15px;
}

label {
    display: block;
    margin-bottom: 5px;
}

input {
    width: 100%;
    padding: 8px;
    margin: 5px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    width: 100%;
    padding: 10px;
    background-color: #42b983;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
}

button:hover {
    background-color: #369f6b;
}
</style>
