<template>
    <div class="signup">
        <h1>Sign Up</h1>
        <form @submit.prevent="handleSubmit">
            <div class="form-group">
                <label for="name">Full Name</label>
                <input type="text" id="name" v-model="name" placeholder="Enter your full name" required />
            </div>
            <div class="form-group">
                <label for="email">Email</label>
                <input type="email" id="email" v-model="email" placeholder="Enter your email" required />
            </div>
            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" id="password" v-model="password" placeholder="Enter your password" required />
            </div>
            <button type="submit">Sign Up</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'SignupPage',
    data() {
        return {
            name: '',
            email: '',
            password: ''
        };
    },
    methods: {
        handleSubmit() {
            // Save user data to localStorage
            const users = JSON.parse(localStorage.getItem('users')) || [];
            const newUser = { name: this.name, email: this.email, password: this.password };

            if (users.some(user => user.email === this.email)) {
                alert('User with this email already exists!');
            } else {
                users.push(newUser);
                localStorage.setItem('users', JSON.stringify(users));
                alert('Sign up successful! You can now log in.');
                this.name = '';
                this.email = '';
                this.password = '';
                this.$router.push('/login'); // Redirect to login page
            }
        }
    }
};
</script>

<style scoped>
.signup {
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
