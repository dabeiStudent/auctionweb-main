<template>
    <div class="container">
        <div class="container-left">
            <a class="header-img" href="/">
                <img class="login-logo" src="../components/HinhAnh/Image/Logo.png" alt="logo">
            </a>
            <img class="login-image-1" src="../components/HinhAnh/Image/Background_Login.png" alt="man">
        </div>
        <div class="container-right">

            <div class="infoUser">
                <h1>Yankee Auction</h1>
                <p class="welcome">Welcome back !!!</p>
                <p class="sign-in">Sign in</p>
                <div class="txt_field">
                    <input type="text" name="name" v-model="name">
                    <span></span>
                    <label>Email</label>
                </div>
                <div class="txt_field">
                    <input type="password" name="password" v-model="password">
                    <span></span>
                    <label>Password</label>
                </div>
                <div class="pass">Forgot Password?</div>
                <input type="submit" value="Login" @click="signin">
                <div class="signup_link">
                    I don’t have an account ? <router-link to="/DangKy">Signup</router-link>
                </div>
            </div>
        </div>
        <hr class="line-login">
    </div>
</template>

<script>
import authenticate from '@/service/authenticate';
import setCookie from '@/service/setCookie';
export default {
    data() {
        return {
            name: '',
            password: ''
        }
    },
    methods: {
        async signin() {
            const response = await authenticate.signin({
                name: this.name,
                password: this.password
            })
            if (response.status == 200) {
                console.log(response.data)
                setCookie('token', response.data)
                this.$router.push('/')
            } else {
                console.log(response.data)
            }
        }
    }

}
</script>

<style scoped>
* {
    padding: 0;
    margin: 0;
}

.infoUser {
    width: 300px;
    height: fit-content;
    box-shadow: 0px 19px 40px rgba(0, 0, 0, 0.05);
    border-radius: 20px;
    padding: 20px 40px;
    margin-top: 10px;
}

.container {
    height: 100vh;
}

.container-left {
    background-color: #FFEDE1;
    float: left;
    width: 40%;
    height: 100%;
    position: relative;
}

.container-right {
    background-color: #FFFFFF;
    float: left;
    width: 60%;
    height: 100%;
    display: flex;
    justify-content: center;
}

.login-logo {
    left: 25%;
    width: 50%;
    top: -5%;
    display: block;
    position: absolute;
}

.login-image-1 {
    bottom: 7%;
    left: 35%;
    width: 80%;
    position: absolute;
}

.line-login {
    width: 100%;
    height: 1px;
    border-width: 0;
    color: #FFCEAE;
    background-color: #FFCEAE;
    position: absolute;
    top: 93%;
}

.infoUser>h1 {
    text-align: center;
    color: #F47458;
    font-family: Poppins, sans-serif;
    filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    padding: 20px 0;
    border-bottom: 0;
}

.sign-in {
    font-family: Poppins, sans-serif;
    font-size: 40px;
    font-weight: bold;
    color: black;
    margin-top: 15px;
}

.welcome {
    font-family: Poppins, sans-serif;
    font-size: 11px;
    font-weight: bold;
    color: rgba(0, 0, 0, 0.5);
}

.txt_field {
    position: relative;
    border-bottom: 2px solid #adadad;
    margin: 30px 0;
}

.txt_field input {
    width: 100%;
    padding: 0 5px;
    height: 30px;
    font-size: 16px;
    border: none;
    background: none;
    outline: none;
}

.txt_field label {
    position: absolute;
    top: -5px;
    left: 5px;
    color: #adadad;
    font-family: Poppins, sans-serif;
    transform: translateY(-50%);
    font-size: 16px;
    /* pointer-events: none; */
    transition: .5s;
}

.txt_field span::before {
    content: '';
    position: absolute;
    top: 30px;
    left: 0;
    width: 0%;
    height: 2px;
    background: #F47458;
    transition: .5s;
}

.txt_field input:focus~label {
    /* top: -5px; */
    color: #F47458;
}

.txt_field input:focus~span::before {
    width: 100%;
}

.pass {
    margin: -5px 0 20px 5px;
    color: #a6a6a6;
    cursor: pointer;
}

.pass:hover {
    text-decoration: underline;
}

input[type="submit"] {
    width: 100%;
    height: 50px;
    border: 1px solid;
    background: #F47458;
    border-radius: 25px;
    font-size: 18px;
    color: #e9f4fb;
    font-weight: 700;
    cursor: pointer;
    outline: none;
}

input[type="submit"]:hover {
    border-color: #2691d9;
    transition: .5s;
}

.signup_link {
    margin: 30px 0;
    text-align: center;
    font-family: Poppins, sans-serif;
    font-size: 11px;
    color: #666666;
}

.signup_link a {
    color: #F47458;
    text-decoration: none;
}

.signup_link a:hover {
    text-decoration: underline;
}
</style>