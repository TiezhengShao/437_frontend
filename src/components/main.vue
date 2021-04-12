<template>
    <div>
        <navbar></navbar>
        <b-container fluid>

        <b-row class="">
                <b-col sm="2" class="col-2">
                    <b-list-group>
                        <b-list-group-item>Filter</b-list-group-item>
                        <b-list-group-item>to be</b-list-group-item>
                        <b-list-group-item>added</b-list-group-item>

                    </b-list-group>

                </b-col>
                    <b-col class="col-10">
                        <b-row class="mt-3 mr-1">
                            <div class="card-deck text-left">
                                <div class="card">
                                    <b-img class="card-img-top"  src="https://files.yande.re/sample/4ead2816e76e5bf11af9a2c912ded33c/yande.re%20752134%20sample%20hatsune_miku%20seifuku%20vocaloid%20yuzuha_wasa.jpg" fluid alt="Fluid image"></b-img>
                                    <div class="card-body">
                                        <h5 class="card-title font-weight-bold"><a href="#">iPhone 12 Pro Max</a></h5>
                                        <h6 class="card-subtitle mb-2 text-info">$999</h6>
                                        <p class="card-text">A very nice iPhone 12 Pro Max</p>
                                    </div>
                                </div>
                                <div class="card">
                                    <b-img class="card-img-top"  src="https://files.yande.re/sample/7d38d192b6a7a605087308bb0e8136be/yande.re%20769135%20sample%20nipples%20no_bra%20pantyhose%20see_through%20t-ravens.jpg" fluid alt="Fluid image"></b-img>
                                    <div class="card-body">
                                        <h5 class="card-title font-weight-bold"><a href="#">iPhone 12 Pro Max</a></h5>
                                        <h6 class="card-subtitle mb-2 text-info">$999</h6>
                                        <p class="card-text">A very nice iPhone 12 Pro Max</p>
                                    </div>
                                </div>
                                <div class="card">
                                    <b-img class="card-img-top"  src="https://files.yande.re/sample/4ead2816e76e5bf11af9a2c912ded33c/yande.re%20752134%20sample%20hatsune_miku%20seifuku%20vocaloid%20yuzuha_wasa.jpg" fluid alt="Fluid image"></b-img>
                                    <div class="card-body">
                                        <h5 class="card-title font-weight-bold"><a href="#">iPhone 12 Pro Max</a></h5>
                                        <h6 class="card-subtitle mb-2 text-info">$999</h6>
                                        <p class="card-text">A very nice iPhone 12 Pro Max</p>
                                    </div>
                                </div>
                            </div>
                        </b-row>

                        <b-row class="mt-3 mr-1">
                            <div class="card-deck text-left">
                                <div class="card">
                                    <b-img class="card-img-top"  src="https://files.yande.re/sample/4ead2816e76e5bf11af9a2c912ded33c/yande.re%20752134%20sample%20hatsune_miku%20seifuku%20vocaloid%20yuzuha_wasa.jpg" fluid alt="Fluid image"></b-img>
                                    <div class="card-body">
                                        <h5 class="card-title font-weight-bold"><a href="#">iPhone 12 Pro Max</a></h5>
                                        <h6 class="card-subtitle mb-2 text-info">$999</h6>
                                        <p class="card-text">A very nice iPhone 12 Pro Max</p>
                                    </div>
                                </div>
                                <div class="card">
                                    <b-img class="card-img-top"  src="https://files.yande.re/sample/4ead2816e76e5bf11af9a2c912ded33c/yande.re%20752134%20sample%20hatsune_miku%20seifuku%20vocaloid%20yuzuha_wasa.jpg" fluid alt="Fluid image"></b-img>
                                    <div class="card-body">
                                        <h5 class="card-title font-weight-bold"><a href="#">iPhone 12 Pro Max</a></h5>
                                        <h6 class="card-subtitle mb-2 text-info">$999</h6>
                                        <p class="card-text">A very nice iPhone 12 Pro Max</p>
                                    </div>
                                </div>
                                <div class="card">
                                    <b-img class="card-img-top"  src="https://files.yande.re/sample/4ead2816e76e5bf11af9a2c912ded33c/yande.re%20752134%20sample%20hatsune_miku%20seifuku%20vocaloid%20yuzuha_wasa.jpg" fluid alt="Fluid image"></b-img>
                                    <div class="card-body">
                                        <h5 class="card-title font-weight-bold"><a href="#">iPhone 12 Pro Max</a></h5>
                                        <h6 class="card-subtitle mb-2 text-info">$999</h6>
                                        <p class="card-text">A very nice iPhone 12 Pro Max</p>
                                    </div>
                                </div>
                            </div>
                        </b-row>
                    </b-col>


            </b-row>
        </b-container>


    </div>

</template>

<script>
    import navbar from "@/components/navbar";
    export default {
        name: "main",
        components: {navbar},
    }
</script>

<style scoped>
    .card-img-top {
        width: 100%;
        height: 12vw;
        object-fit: cover;
    }
    a { text-decoration: none; }

</style>