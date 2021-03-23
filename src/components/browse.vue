<template>
<b-container>
  <body class="text-center">
  <div>
  <b-card-group deck>
    <!-- <b-card title="Title" img-src="https://picsum.photos/300/300/?image=41" img-alt="Image" img-top>
      <b-card-text>
        This is a wider card with supporting text below as a natural lead-in to additional content.
        This content is a little bit longer.
      </b-card-text>
    </b-card> -->

    <b-card title="Title" >
      <b-card-text>
        This card has supporting text below as a natural lead-in to additional content.
      </b-card-text>
    </b-card>

    <b-card title="Title" >
      <b-card-text>
        This is a wider card with supporting text below as a natural lead-in to additional content.
        This card has even longer content than the first to show that equal height action.
      </b-card-text>
    </b-card>

    <b-card title="Title" >
      <b-card-text>
        This is a wider card with supporting text below as a natural lead-in to additional content.
        This card has even longer content than the first to show that equal height action.
      </b-card-text>
    </b-card>
  </b-card-group>
</div>
</body>
</b-container>

</template>

<script>
    export default {
        name: "browse",
        methods: {
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