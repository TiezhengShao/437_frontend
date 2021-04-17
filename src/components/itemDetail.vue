<template>
    <div>
        <navbar></navbar>

        <b-container fluid>
            <!-- Stack the columns on mobile by making one full-width and the other half-width -->
            <b-row  class="pt-4">
                <b-col cols="12" md="8">
                    <b-container class="mt-3" >
                        <h3 class="my-3 font-weight-bold">Item Image</h3>
                        <b-img class="item-image-box" src="https://files.yande.re/sample/e1f9f353dd281ad9e6f3fc5d37ccce9e/yande.re%20761173%20sample%20monaka_curl%20morino_rinze%20seifuku%20the_idolm%40ster%20the_idolm%40ster_shiny_colors.jpg"  fluid alt="Fluid-grow image" rounded></b-img>
                    </b-container>
                </b-col>

                <b-col class="border-left text-left pt-4" cols="6" md="4" >
                    <H3 class="mb-3" v-model="itemName">iPhone 12 Pro Max</H3>

                    <H5 >Price:</H5>
                    <p><span>$1234</span></p>

                    <H5 class="mb-3">Description:</H5>
                    <div class="overflow-auto">
                        <p>Of course, even when you get home, you’re probably still on the go, whether it’s scrambling to make dinner, chasing after the kids — or even bigger projects, like trying to add tech to your remodel of a current space or looking for tips when moving to the next one. Whatever you’re working on, upgrading the technology for your home can bring a little less hassle — and a little more excitement — to your everyday routine.</p>
                    </div>

                        <b-button variant="success" class="btn-lg btn-block mb-3" @click="onPostItemBtnClick()" type="submit">I'm interested, e-mail seller!</b-button>

                    <b-alert
                            :show="dismissCountDown" dismissible variant="success" @dismissed="dismissCountDown=0" @dismiss-count-down="countDownChanged">
                        {{ submitMsg }}
                    </b-alert>
                </b-col>
            </b-row>
        </b-container>
    </div>
</template>

<script>
    import navbar from "@/components/navbar";

    export default {
        name: "itemDetail",
        components: {navbar},
        data() {
            return {
                dismissSecs: 5,
                dismissCountDown: 0,
                submitMsg: '',
                itemName:''
            }
        },
        methods:{
            countDownChanged(dismissCountDown) {
                this.dismissCountDown = dismissCountDown
            },
            showAlert() {
                this.dismissCountDown = this.dismissSecs
            },
            onPostItemBtnClick(){
                this.submitMsg = "Successful";
                this.showAlert();
            }
        }

    }
</script>

<style scoped>
    .item-image-box {
        width: 100%;
        height: 39vw;
        object-fit: contain;
    }
</style>