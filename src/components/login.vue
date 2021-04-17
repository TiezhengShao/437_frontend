<template>
<b-container>

    <b-alert
            :show="mainDismissCountDown" dismissible variant="danger" @dismissed="mainDismissCountDown=0" @dismiss-count-down="mainCountDownChanged">
        {{ errorMsg }}
    </b-alert>

    <body class="text-center">
    <form class="form-signin">
        <img class="mb-4" src="../assets/market-logo.svg" alt="" width="72" height="57">
        <h1 class="h3 mb-3 font-weight-normal">Welcome to WashU Student Marketplace</h1>
        <b-input-group append="@wustl.edu">

            <b-form-input id="email-sign-up" v-model="email" placeholder="E-mail address" type="text"  required></b-form-input>
        </b-input-group>

        <b-form-input id="input-2" v-model="password" type="password" autocomplete="on" placeholder="Password" required></b-form-input>

        <div class="form-group d-md-flex">
            <div class="w-50 text-md-left">
                <b-link v-b-modal.modal-sign-up href="#foo">Sign me up!</b-link>
            </div>
            <div class="w-50 text-md-right">
                <b-link v-b-modal.modal-pwd-recovery href="#foo">Forget password?</b-link>
            </div>
        </div>
        <b-button variant="primary" class="btn-lg btn-block" @click="onSignInBtnClick()" >Sign in</b-button>

    </form>
    </body>



    <b-modal id="modal-sign-up" ref="modal" title="Sign up" @show="resetSignUpModal" @hidden="resetSignUpModal" @ok="handleOk">
        <form ref="form" @submit.stop.prevent="handleSubmit">
            <b-form-group label="WashU E-mail address" label-for="email-sign-up" invalid-feedback="WashU E-mail address is required">
                <b-input-group append="@wustl.edu">
                    <b-form-input id="email-sign-up" v-model="emailSignUp"  type="text"  required></b-form-input>
                </b-input-group>
            </b-form-group>
            <b-form-group label="Password" label-for="password-sign-up" invalid-feedback="Password is required">
                <b-form-input id="password-sign-up" v-model="pwdSignUp" type="password" autocomplete="off" required></b-form-input>
            </b-form-group>
            <b-form-group label="Repeat Password" label-for="passwordR-sign-up" invalid-feedback="Password does not match">
                <b-form-input id="passwordR-sign-up" v-model="pwdRSignUp" type="password" autocomplete="off" required></b-form-input>
            </b-form-group>
        </form>
        <b-alert
                :show="dismissCountDown" dismissible variant="danger" @dismissed="dismissCountDown=0" @dismiss-count-down="countDownChanged">
            {{ errorMsg }}
        </b-alert>
    </b-modal>

    <b-modal id="modal-pwd-recovery" ref="modal" title="Forget Password" @show="resetPRModal" @hidden="resetPRModal" @ok="handlePROk">
        <form ref="form" @submit.stop.prevent="handleSubmit">
            <b-form-group label="WashU E-mail address" label-for="email-PR">
                <b-input-group append="@wustl.edu">
                    <b-form-input id="email-PR" v-model="emailPR"  type="text"  required></b-form-input>
                </b-input-group>
            </b-form-group>
            <div class="w-50 text-md-left">
                <b-link v-b-modal.modal-pwd-reset href="#foo">Already get a token?</b-link>
            </div>
        </form>
        <b-alert
                :show="prDismissCountDown" dismissible variant="danger" @dismissed="prDismissCountDown=0" @dismiss-count-down="prCountDownChanged">
            {{ errorMsg }}
        </b-alert>
    </b-modal>

    <b-modal id="modal-pwd-reset" ref="modal" title="Reset Your Password" @show="resetPRstModal" @hidden="resetPRstModal" @ok="handlePwdRstROk">
        <form ref="form" @submit.stop.prevent="handleSubmit">
            <b-form-group label="Token" label-for="token-pwd-rst">
                <b-form-input id="token-pwd-rst" v-model="tokenPwdRst" type="text" autocomplete="off" required></b-form-input>
            </b-form-group>
            <b-form-group label="Password" label-for="password-pwd-rst">
                <b-form-input id="password-pwd-rst" v-model="pwdPwdRst" type="password" autocomplete="off" required></b-form-input>
            </b-form-group>
            <b-form-group label="Repeat Password" label-for="passwordR-pwd-rst">
                <b-form-input id="passwordR-pwd-rst" v-model="pwdRPwdRst" type="password" autocomplete="off" required></b-form-input>
            </b-form-group>
        </form>
        <b-alert
                :show="pRstDismissCountDown" dismissible variant="danger" @dismissed="pRstDismissCountDown=0" @dismiss-count-down="pRstCountDownChanged">
            {{ errorMsg }}
        </b-alert>
    </b-modal>


</b-container>

</template>

<script>
    import axios from 'axios'

    export default {
        name: "login",
        data() {
            return {
                email:'',
                password:'',
                emailSignUp:'',
                pwdSignUp:'',
                pwdRSignUp:'',
                emailPR:'',
                tokenPwdRst:'',
                pwdPwdRst:'',
                pwdRPwdRst:'',
                errorMsg:'',
                dismissSecs: 5,
                dismissCountDown: 0,
                mainDismissSecs: 5,
                mainDismissCountDown: 0,
                prDismissSecs: 5,
                prDismissCountDown: 0,
                pRstDismissSecs: 5,
                pRstDismissCountDown: 0,
                MsgBox: '',
            }
        },

        methods:{
            showMsgBox(title, content) {
                this.boxOne = '';
                this.$bvModal.msgBoxOk(content, {
                    title: title,
                    okVariant: 'primary',
                    headerClass: 'p-2 border-bottom-0',
                    footerClass: 'p-2 border-top-0',
                    centered: true
                })
                    .then(value => {
                        this.boxTwo = value
                    })

            },
            countDownChanged(dismissCountDown) {
                this.dismissCountDown = dismissCountDown
            },
            showAlert() {
                this.dismissCountDown = this.dismissSecs
            },
            mainCountDownChanged(mainDismissCountDown) {
                this.mianDismissCountDown = mainDismissCountDown
            },
            showMainAlert() {
                this.mainDismissCountDown = this.mainDismissSecs
            },
            prCountDownChanged(prDismissCountDown) {
                this.prDismissCountDown = prDismissCountDown
            },
            showPRAlert() {
                this.prDismissCountDown = this.prDismissSecs
            },
            pRstCountDownChanged(pRstDismissCountDown) {
                this.pRstDismissCountDown = pRstDismissCountDown
            },
            showPRstAlert() {
                this.pRstDismissCountDown = this.pRstDismissSecs
            },
            checkSignupForm(){
                if(this.emailSignUp.length >= 1){
                    if(this.pwdRSignUp.length >= 3 ){
                        if(this.pwdSignUp === this.pwdRSignUp){
                            console.log("Check successful");
                            return true;
                        }
                        else {
                            this.errorMsg = 'Password does not match';
                            console.log("Check unsuccessful");
                            this.showAlert();
                            return false;
                        }
                    }
                    else {
                        this.errorMsg = 'Password must be 3 character or longer';
                        console.log("Check unsuccessful");
                        this.showAlert();
                        return false;
                    }

                }
                else {
                    this.errorMsg = 'Please enter a valid e-mail address';
                    console.log("Check unsuccessful");
                    this.showAlert();
                    return false;
                }

            },
            checkPwdRstForm(){
                if(this.tokenPwdRst.length >= 10){
                    if(this.pwdPwdRst.length >= 3 ){
                        if(this.pwdPwdRst === this.pwdRPwdRst){
                            console.log("Check successful");
                            return true;
                        }
                        else {
                            this.errorMsg = 'Password does not match';
                            console.log("Check unsuccessful");
                            this.showPRstAlert();
                            return false;
                        }
                    }
                    else {
                        this.errorMsg = 'Password must be 3 character or longer';
                        console.log("Check unsuccessful");
                        this.showPRstAlert();
                        return false;
                    }

                }
                else {
                    this.errorMsg = 'Please enter a valid token in your e-mail';
                    console.log("Check unsuccessful");
                    this.showPRstAlert();
                    return false;
                }

            },
            checkPRForm(){
                if(this.emailPR.length >= 1) {
                    console.log("Check PR successful");
                    return true;
                }
                console.log("Check PR unsuccessful");
                return false;

                },
            checkSignInForm(){
                if(this.email.length >= 1 && this.password.length >= 3) {
                    console.log("Check SignIn successful");
                    return true;
                }
                console.log("Check SignIn unsuccessful");
                return false;

            },
            resetSignUpModal() {
                this.emailSignUp = '';
                this.pwdSignUp = '';
                this.pwdRSignUp = '';
                this.errorMsg = '';
            },
            resetPRModal() {
                this.emailPR = '';
                this.errorMsg = '';
            },
            resetPRstModal() {
                this.tokenPwdRst = '';
                this.pwdPwdRst = '';
                this.pwdRPwdRst = '';
                this.errorMsg = '';
            },
            handleOk(bvModalEvt) {
                // Prevent modal from closing
                bvModalEvt.preventDefault();
                if(this.checkSignupForm() === true){
                    var signUpJSON = {"LoginName": this.emailSignUp,"HashedPassword":this.pwdSignUp};
                    this.fetchData(2,signUpJSON);
                }
                else {
                    bvModalEvt.preventDefault();
                }
            },
            handlePROk(bvModalEvt) {
                // Prevent modal from closing
                bvModalEvt.preventDefault();
                if (this.checkPRForm() === true) {
                    this.getCloudDataGET(this.emailPR);
                } else {
                    this.errorMsg = 'Please enter a valid e-mail address. ';
                    this.showPRAlert();
                }
            },
            handlePwdRstROk(bvModalEvt) {
                // Prevent modal from closing
                bvModalEvt.preventDefault();
                if(this.checkPwdRstForm() === true){
                    let pwdRstJSON = {"Token": this.tokenPwdRst,"HashedPassword":this.pwdPwdRst};
                    console.log(pwdRstJSON)
                    this.fetchData(4,pwdRstJSON);
                }
                else {
                    bvModalEvt.preventDefault();
                }
            }
            ,
            onSignInBtnClick(){
                //console.log(this.email);
                var aClickJSON = {"LoginName": this.email,"HashedPassword":this.password};
                this.fetchData(1, aClickJSON);
                //this.onSignInError();
            },
            onSignInError(){
                this.errorMsg = 'Login certificate error or you have not verified your account yet, please try again';
                this.showMainAlert();
            },
            onSignInSuccess(){
                this.errorMsg = 'Sign in successful, redirecting...';
                this.showMainAlert();
            }
        ,
            // type 1->sign in, 2->sign up, 3->Password Recovery, 4->Password Reset
            fetchData(type, json){
                console.log(JSON.stringify(json));
                var link = 'http://165.232.138.223:8080/auth/user/login';
                if(type === 2){
                    link = 'http://165.232.138.223:8080/auth/user/signup';
                }
                if(type === 4){
                    link = 'http://165.232.138.223:8080/auth/user/update';
                }
                console.log('link:' + link);

                fetch(link, {
                    method: 'POST',
                    body: JSON.stringify(json),
                    headers: {
                        'Content-Type': 'application/json'
                    },
                }).then(response => response.json())
                    .then(data => {
                        console.log(data);
                        if(type === 1){
                            // TODO

                            // here we have to add user and jwt, modify to show what data backend returns
                            // localStorage.setItem('user',JSON.stringify(response.data.user))
                            var now = new Date().getTime();
                            localStorage.setItem('expire',now);
                            localStorage.setItem('jwt',data.Token);

                            this.onSignInSuccess();
                            this.$router.push({ path: '/browse' })
                        }else if(type === 2){
                            this.$bvModal.hide('modal-sign-up');
                            this.showMsgBox('Your Account has been created', 'A verification e-mail should has been sent to your' +
                                ' Washington University e-mail address. Please Complete verification as soon as possible. ');
                        }
                        else if(type === 4){
                            console.log("Password recovery successful.")
                        }else if(type === -1){
                            console.log("Fetch type error")
                        }
                    }).catch(error=>{
                        console.log(error);
                        if(type === 1){
                            this.onSignInError();
                        } else if(type === 2){
                            this.errorMsg = 'Account already exist. ';
                            this.showAlert();
                        }
                        else if(type === 4){
                            console.log("Password recovery server error response.")
                        }
                        },

                );
            },

            getCloudDataGET(data){
                var link = 'http://165.232.138.223:8080/auth/user/recover?username=' + data;
                console.log('link:' + link);
                axios.get(link)
                    .then((response) =>{
                        console.log(response);
                        //this.$bvModal.hide('modal-pwd-recovery');
                        this.showMsgBox('Requested E-mail Sent', 'If you have an account associated with this address, you will receive an temporary password via e-mail shortly. ');
                        }
                    )
                    .catch(error => {
                        this.errorMessage = error.message;
                        console.error("error: ", error);
                        this.errorMsg = 'Server communication error try later';
                        this.showPRAlert();
                    });
            }
            ,
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
        margin-bottom: -1px;
        border-bottom-right-radius: 0;
        border-bottom-left-radius: 0;
    }
    .form-signin input[type="password"] {
        margin-bottom: 10px;
        border-top-left-radius: 0;
        border-top-right-radius: 0;
    }
</style>