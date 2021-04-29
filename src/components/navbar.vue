<template>
    <div class="pb-2">
        <b-navbar toggleable="lg" type="dark" variant="info" sticky >
            <b-navbar-brand href="#" @click="onTitleClick()">WashU Marketplace</b-navbar-brand>

                <form class="form-inline mt-2 mt-md-0">
                    <input class="form-control mr-sm-2" type="text" v-model="keyword" placeholder="Search" aria-label="Search">
                    <button class="btn btn-outline-light my-2 my-sm-0" @click.prevent="onSearchClick()">Search</button>
                </form>


            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

            <b-collapse id="nav-collapse" is-nav>

                <!-- Right aligned nav items -->
                <b-navbar-nav class="ml-auto">
                    <b-navbar-nav>

                        <ul class="navbar-nav mr-auto">
                            <li class="nav-item">
                                <a class="nav-link " @click="onSellClick()" href="#" tabindex="-1" aria-disabled="true">Sell</a>
                            </li>
                            <li class="nav-item">
                                <a class="nav-link " @click="onListClick()" href="#" tabindex="-1" aria-disabled="true">My Listing</a>
                            </li>
<!--                            <li class="nav-item">
                                <a class="nav-link" href="#">Username</a>
                            </li>-->
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
                keyword:'',
                curr_time: null,
            }
        },
        mounted(){
            this.$emit("event", this.keyword)
        }
        ,
        created() {
            setInterval(this.getNow, 1000);
        },
        methods:{
            onTitleClick(){
                console.log("path:" + this.$router.currentRoute.path);
                if(this.$router.currentRoute.path === '/browse'){
                    this.$router.go(0);
                } else {
                    this.$router.push({ path: "/browse", query:{keyword:''}}).then(this.$forceUpdate());
                }
            },
            onSearchClick(){
                this.$emit("searchEvent", this.keyword);
                this.$emit("newItemSearchEvent", this.keyword);
                this.$emit("detailSearchEvent", this.keyword);
                this.$emit("listSearchEvent", this.keyword);
            },
            onSellClick(){
                this.$router.push({ path: "/new" }).then(this.$forceUpdate());

            },
            onListClick(){
                this.$router.push({ path: "/list" }).then(this.$forceUpdate());
            },
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