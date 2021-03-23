<template>
<b-container>
    <body class="text-center">
    <form class="form-signin">
        <img class="mb-4" src="../assets/market-logo.svg" alt="" width="72" height="57">
        <h1 class="h3 mb-3 font-weight-normal">Welcome to WashU Student Marketplace</h1>
        <label for="username" class="sr-only">Username</label>
        <input type="username" id="inputUsername" class="form-control" placeholder="Username" required autofocus>
        <label for="inputPassword" class="sr-only">Password</label>
        <input type="password" id="inputPassword" class="form-control" placeholder="Password" required>
        <label for="inputPassword" class="sr-only">Confirm Password</label>
        <input type="password" id="inputPassword" class="form-control" placeholder="Confirm password" required>
        <label for="inputEmail" class="sr-only">Email address</label>
        <input type="email" id="inputEmail" class="form-control" placeholder="email@wustl.edu" required>
        <button class="btn btn-lg btn-primary btn-block" type="submit">Sign up</button>
        <p class="mt-5 mb-3 text-muted">&copy; 2017-2020</p>
    </form>
    </body>
</b-container>

</template>

<script>
    export default {
        name: "signup"
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