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
            <b-form-input id="email-sign-up" v-model="email" placeholder="E-mail address" type="email"  required></b-form-input>
        </b-input-group>
        <b-form-input id="input-2" v-model="password" type="password" placeholder="Password" required></b-form-input>
<!--        <div class="checkbox mb-3">
            <label>
                <input type="checkbox" value="remember-me"> Remember me
            </label>
        </div>-->

        <div class="form-group d-md-flex">
            <div class="w-50 text-md-left">
                <b-link v-b-modal.modal-sign-up href="#foo">Sign me up!</b-link>
            </div>
            <div class="w-50 text-md-right">
                <b-link v-b-modal.modal-pwd-recovery href="#foo">Forget password?</b-link>
            </div>
        </div>
        <b-button variant="primary" class="btn-lg btn-block" @click="onSignInBtnClick()" type="submit">Sign in</b-button>

    </form>
    </body>



    <b-modal id="modal-sign-up" ref="modal" title="Sign up" @show="resetSignUpModal" @hidden="resetSignUpModal" @ok="handleOk">
        <form ref="form" @submit.stop.prevent="handleSubmit">
            <b-form-group label="WashU E-mail address" label-for="email-sign-up" invalid-feedback="WashU E-mail address is required">
                <b-input-group append="@wustl.edu">
                    <b-form-input id="email-sign-up" v-model="emailSignUp"  type="email"  required></b-form-input>
                </b-input-group>
            </b-form-group>
            <b-form-group label="Password" label-for="password-sign-up" invalid-feedback="Password is required">
                <b-form-input id="password-sign-up" v-model="pwdSignUp" type="password" required></b-form-input>
            </b-form-group>
            <b-form-group label="Repeat Password" label-for="passwordR-sign-up" invalid-feedback="Password does not match">
                <b-form-input id="passwordR-sign-up" v-model="pwdRSignUp" type="password" required></b-form-input>
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
                    <b-form-input id="email-PR" v-model="emailPR"  type="email"  required></b-form-input>
                </b-input-group>
            </b-form-group>
        </form>
    </b-modal>


</b-container>

</template>

<script>
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
                errorMsg:'',
                dismissSecs: 3,
                dismissCountDown: 0,
                mainDismissSecs: 5,
                mainDismissCountDown: 0,
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
            checkPRForm(){
                if(this.emailPR.length >= 1) {
                    console.log("Check PR successful");
                    return true;
                }
                console.log("Check PR unsuccessful");
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
            handleOk(bvModalEvt) {
                // Prevent modal from closing
                if(this.checkSignupForm() === false){
                    this.showMsgBox('Your Account has been created', 'A verification e-mail should has been sent to your' +
                        ' Washington University e-mail address. Please Complete verification as soon as possible. ');
                }
                else {
                    bvModalEvt.preventDefault();
                }
            },
            handlePROk(bvModalEvt) {
                // Prevent modal from closing
                if (this.checkSignupForm() === false) {
                    this.showMsgBox('Requested E-mail Sent', 'If you have an account associated with this address, you will receive an temporary password via e-mail shortly. ');
                } else {
                    bvModalEvt.preventDefault();
                }
            }
            ,
            onSignInBtnClick(){
                console.log(this.email);
                //this.fetchData();
                this.onSignInError();
            },
            onSignInError(){
                this.errorMsg = 'E-mail address or password does not match or record, please try again';
                this.showMainAlert();
            }
        ,
            fetchData(){
                var aClickJSON = {"cmd": "getRealTime","val":1};
                fetch('https://webhook.site/30ff11fd-2a73-455e-9469-32109732faf5', {
                    method: 'post',
                    body: JSON.stringify(aClickJSON)
                }).then(response => response.json())
                    .then(data => {
                        this.genTable(data);
                        //this.consoleOut(data);
                    });
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