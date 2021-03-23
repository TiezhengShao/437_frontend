<template>
<b-container>
    <b-alert
            :show="dismissCountDown" dismissible variant="danger" @dismissed="dismissCountDown=0" @dismiss-count-down="countDownChanged">
        {{ errorMsg }}
    </b-alert>
    <body class="text-center">
    <form class="form-signin">
        <img class="mb-4" src="../assets/password.png" alt="" width="80" height="80">
        <h1 class="h3 mb-3 font-weight-normal">Reset your password</h1>
        <b-form-input id="token" v-model="token" type="password" autocomplete="off" placeholder="Token" required></b-form-input>
        <b-form-input id="password" v-model="password" type="password" autocomplete="off" placeholder="Password" required></b-form-input>
        <b-form-input id="rPassword" v-model="rPassword" type="password" autocomplete="off" placeholder="Repeat Password" required></b-form-input>

        <button class="btn btn-lg btn-primary btn-block mt-3" @click="onRestBtnClick()">Reset</button>

    </form>



    </body>

</b-container>

</template>

<script>
    export default {
        name: "pwdRst",
        data() {
            return {
                token:'',
                password:'',
                rPassword:'',
                errorMsg:'',
                dismissSecs: '',
                dismissCountDown: 0,
                MsgBox: '',
            }
        },
        methods:{
            onRestBtnClick(){
                this.checkPRForm();
                console.log("Clicked");

            },
            countDownChanged(dismissCountDown) {
                this.dismissCountDown = dismissCountDown
            },
            showAlert() {
                this.dismissCountDown = this.dismissSecs
            },
            checkPRForm(){
                if(this.token >= 10) {
                    if(this.password.length >= 3){
                        if(this.password.length === this.rPassword){
                            return true
                        }else {
                            this.errorMsg = 'Password does not match';
                            console.log("Check unsuccessful");
                            this.showAlert();
                            return false
                        }
                    }else{
                        this.errorMsg = 'Password is too short';
                        console.log("Check unsuccessful");
                        this.showAlert();
                        return false
                    }
                }else{
                    this.errorMsg = 'Token is too short';
                    console.log("Check unsuccessful");
                    this.showAlert();
                    return false;
                }

            },
        }

    }
</script>

<style scoped>
    .bd-placeholder-img {
        font-size: 1.125rem;
        text-anchor: middle;
        -webkit-user-select: none;
        -moz-user-select: none;
        user-select: none;
    }

    @media (min-width: 768px) {
        .bd-placeholder-img-lg {
            font-size: 3.5rem;
        }
    }

    html,
    body {
        height: 100%;
    }

    body {
        display: -ms-flexbox;
        display: flex;
        -ms-flex-align: center;
        align-items: center;
        padding-top: 40px;
        padding-bottom: 40px;
    }

    .form-signin {
        width: 100%;
        max-width: 330px;
        padding: 15px;
        margin: auto;
    }
    .form-signin .checkbox {
        font-weight: 400;
    }
    .form-signin .form-control {
        position: relative;
        box-sizing: border-box;
        height: auto;
        padding: 10px;
        font-size: 16px;
    }
    .form-signin .form-control:focus {
        z-index: 2;
    }
    .form-signin input[type="email"] {
        margin-bottom: 10px;
        border-bottom-right-radius: 0;
        border-bottom-left-radius: 0;
    }
    .form-signin input[type="password"] {
        margin-bottom: -1px;
        border-top-left-radius: 0;
        border-top-right-radius: 0;
    }
    .form-signin input[type="username"] {
        margin-bottom: -1px;
        border-top-left-radius: 0;
        border-top-right-radius: 0;
    }

</style>