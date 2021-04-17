<template>
    <div>
        <b-navbar toggleable="lg" type="dark" variant="dark" fixed="top">
            <b-navbar-brand href="#">WashU Marketplace</b-navbar-brand>

                <form class="form-inline mt-2 mt-md-0">
                    <input class="form-control mr-sm-2" type="text" placeholder="Search" aria-label="Search">
                    <button class="btn btn-outline-light my-2 my-sm-0" type="submit">Search</button>
                </form>


            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

            <b-collapse id="nav-collapse" is-nav>

                <!-- Right aligned nav items -->
                <b-navbar-nav class="ml-auto">
                    <b-navbar-nav>

                        <ul class="navbar-nav mr-auto">
                            <li class="nav-item">
                                <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Sell</a>
                            </li>
                            <li class="nav-item">
                                <a class="nav-link" href="#">Username</a>
                            </li>
                            <li class="nav-item">
                                <a class="nav-link"  @click="onLogoutClick()" href="#">Logout</a>
                            </li>
                        </ul>
                    </b-navbar-nav>
                </b-navbar-nav>
            </b-collapse>
        </b-navbar>
    </div>
</template>

<script>
    export default {
        name: "navbar",

        data:function () {
            return{
                curr_time: null,
            }
        },
        created() {
            setInterval(this.getNow, 1000);
        },
        methods:{
            onLogoutClick(){
                localStorage.clear();
                console.log("session cleared, logged out! ");
                window.location.reload();
            }
        }
    }
</script>

<style scoped>

</style>