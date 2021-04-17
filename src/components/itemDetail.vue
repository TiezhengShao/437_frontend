<template>
    <div>
        <navbar></navbar>

        <b-container fluid>
            <!-- Stack the columns on mobile by making one full-width and the other half-width -->
            <b-row  class="pt-4">
                <b-col cols="12" md="8">
                    <b-container class="mt-3" >
                        <h3 class="my-3 font-weight-bold">Item Image</h3>
                        <b-img class="item-image-box" :src="itemImage"  fluid alt="Fluid-grow image" rounded></b-img>
                    </b-container>
                </b-col>

                <b-col class="border-left text-left pt-4" cols="6" md="4" >
                    <H3 class="mb-3">{{itemName}}</H3>

                    <H5 >Price:</H5>
                    <p><span >${{itemPrice}}</span></p>

                    <H5 class="mb-3">Description:</H5>
                    <div class="overflow-auto">
                        <p>{{itemDesc}}</p>
                    </div>

                        <b-button variant="success" class="btn-lg btn-block mb-3" @click="onContactSellerBtnClick()" type="submit">I'm interested, e-mail seller!</b-button>

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
    import axios from "axios";

    export default {
        name: "itemDetail",
        components: {navbar},
        data() {
            return {
                dismissSecs: 5,
                dismissCountDown: 0,
                submitMsg: '',
                itemName:'Undefined',
                itemImage:'',
                itemPrice:'Undefined',
                itemDesc:'Undefined'
            }
        },
        mounted() {
            this.getCloudDataGET(this.$route.params.id);
            //console.log("item mounted")
            console.log(this.$route.params.id);
        },
        methods:{
            countDownChanged(dismissCountDown) {
                this.dismissCountDown = dismissCountDown
            },
            showAlert() {
                this.dismissCountDown = this.dismissSecs
            },
            onContactSellerBtnClick(){
                this.submitMsg = "Successful";
                this.showAlert();
            },
            fetchData(){
                let json = {Tags: [this.$route.params.id]};
                console.log(JSON.stringify(json));
                var link = 'http://165.232.138.223:8080/item/get';
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
                        this.title = data.items[0].Title
                        this.text = data.items[0].Description
                        console.log(data);
                    }).catch(error=>{
                        console.log(error);
                    }
                )
            },
            getCloudDataGET(data){
                var link = 'http://165.232.138.223:8080/item/detail?obj_id=' + data;
                console.log('link:' + link);
                axios.get(link)
                    .then((response) =>{
                            console.log(response.data.Items[0]);
                            let item = response.data.Items[0];
                            let image = item.Images[0];
                            if(item !== undefined){
                                this.itemName = item.Title;
                                this.itemPrice = item.NewPrice;
                                this.itemDesc = item.Description;
                                if(item.Description.length < 1){
                                    this.itemDesc = "No description provided by uploader."
                                }
                                if(image !== undefined){
                                    this.itemImage = "data:image/png;base64," + image;
                                }
                                //console.log(item.Images[0]);
                            }else {
                                // Not get item from server
                                console.log("Server returns nothing" + response);
                            }
                            //this.showMsgBox('Requested E-mail Sent', 'If you have an account associated with this address, you will receive an temporary password via e-mail shortly. ');
                        }
                    )
                    .catch(error => {
                        this.errorMessage = error.message;
                        console.error("error: ", error);
                    });
            }
            ,
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