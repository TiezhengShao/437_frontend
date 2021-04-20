<template>
    <div>
        <navbar @detailSearch_event="search"></navbar>

        <b-container fluid>
            <!-- Stack the columns on mobile by making one full-width and the other half-width -->
            <b-row  class="pt-4">
                <b-col cols="12" md="8">
                    <b-container class="mt-3" >
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

                    <b-button-group>
                        <b-button variant="outline-success"  @click="onContactSellerBtnClick()" type="submit">Contact Seller</b-button>
                        <b-dropdown variant="outline-secondary" right text="Edit">
                            <b-dropdown-item @click="onDelBtnClicked()">Delete</b-dropdown-item>
                        </b-dropdown>

                    </b-button-group>

                    <b-alert class="mt-3"
                            :show="dismissCountDown" dismissible :variant="variant" @dismissed="dismissCountDown=0" @dismiss-count-down="countDownChanged">
                        {{ alertMsg }}
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
                objId:'',
                token:'',
                uploaderId:0,
                alertMsg: '',
                itemName:'Undefined',
                itemImage:'',
                itemPrice:'Undefined',
                itemDesc:'Undefined',
                variant : "success",
            }
        },
        mounted() {
            this.objId = this.$route.params.id;
            this.token = localStorage.getItem('jwt');

            let link = 'http://165.232.138.223:8080/item/detail?obj_id=' + this.objId;
            this.getCloudDataGET(link);
            //console.log("item mounted")
            console.log(this.$route.params.id);
        },
        methods:{
            search(keyword){
                this.$router.push({ path: '/browse' , query:{keyword:keyword}});
            },
            onDelBtnClicked(){
                let json = {Token:this.token, ObjId: this.objId};
                let link = 'http://165.232.138.223:8080/item/delete';
                this.fetchData(json, link, 2);
            },
            countDownChanged(dismissCountDown) {
                this.dismissCountDown = dismissCountDown
            },
            showAlert() {
                this.dismissCountDown = this.dismissSecs
            },
            onContactSellerBtnClick(){
                let json = {Token:this.token,ItemTitle:this.itemName, UploaderId:parseInt(this.uploaderId) , ObjId: this.objId};
                let link = 'http://165.232.138.223:8080/item/user/contact';
                this.fetchData(json, link, 1)

            },
            fetchData(json, link, type){
                // type 1:contact, 2:delete
                console.log(JSON.stringify(json));
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
                            this.variant = "success";
                            this.alertMsg = "Notification e-mail sent, please wait for seller's response. ";
                            this.showAlert();
                        }
                        if(type === 2){
                            this.$router.push({ path: '/browse' });
                        }
                    }).catch(error=>{
                        console.log(error);
                        this.variant = "danger";
                        if(type === 1){
                            this.alertMsg = "Server contact error, try again later";
                        }
                        if(type === 2){
                            this.alertMsg = "Cannot delete if not the uploader.";
                        }
                        this.showAlert();
                        //this.variant = "success";
                    }
                )
            },
            getCloudDataGET(link){
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
                                this.uploaderId = item.Uploader;

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