<template>
    <div>
        <navbar></navbar>

        <b-container>
            <!-- Stack the columns on mobile by making one full-width and the other half-width -->
            <b-row  class="pt-4">
                <b-col cols="12" md="8">
                    <b-container class="mt-3" fluid >
                        <image-uploader
                                :preview="true"
                                :className="['fileinput', { 'fileinput--loaded': hasImage }]"
                                :maxWidth="2048"
                                :quality="0.9"
                                :debug="1"
                                doNotResize="gif"
                                :autoRotate="true"
                                outputFormat="string"
                                @input="setImage"
                        >

                        </image-uploader>
                        <label for="fileInput" slot="upload-label">
                            <figure>
                                <img
                                        src="https://img.icons8.com/plasticine/100/000000/image.png"
                                        width="80"
                                        height="80"
                                >
                                <path
                                        class="path1"
                                        d="M9.5 19c0 3.59 2.91 6.5 6.5 6.5s6.5-2.91 6.5-6.5-2.91-6.5-6.5-6.5-6.5 2.91-6.5 6.5zM30 8h-7c-0.5-2-1-4-3-4h-8c-2 0-2.5 2-3 4h-7c-1.1 0-2 0.9-2 2v18c0 1.1 0.9 2 2 2h28c1.1 0 2-0.9 2-2v-18c0-1.1-0.9-2-2-2zM16 27.875c-4.902 0-8.875-3.973-8.875-8.875s3.973-8.875 8.875-8.875c4.902 0 8.875 3.973 8.875 8.875s-3.973 8.875-8.875 8.875zM30 14h-4v-2h4v2z"
                                ></path>
                            </figure>
                            <span class="upload-caption">{{
            hasImage ? "Replace" : "Click to upload your item image"
          }}</span>
                        </label>
                    </b-container>
                </b-col>

                <b-col class="border-left" cols="6" md="4" >
                    <H3 class="text-left mb-3">Item Information</H3>

                    <form class="form-item-post"  >
                        <b-form-input id="input-2" v-model="itemName" type="text" placeholder="Name" class="mb-2" required></b-form-input>

                        <b-input-group prepend="$" class="mb-2" >
                            <b-form-input id="item-price" v-model="itemPrice" placeholder="123.45" type="number" required></b-form-input>
                        </b-input-group>

                        <b-form-tags class="mb-2" input-id="tags-basic" v-model="tagValue"></b-form-tags>

                        <b-form-textarea
                                id="textarea"
                                v-model="itemDetail"
                                placeholder="Item description"
                                rows="3"
                                max-rows="6"
                                class="mb-2"
                        ></b-form-textarea>

                        <p class="text-left">Tips: Buyers would contact you using your WashU e-mail address.</p>

                        <b-button variant="success" class="btn-lg btn-block" @click="onPostItemBtnClick" type="submit">Publish</b-button>

                    </form>
                    <b-alert
                            :show="dismissCountDown" dismissible variant="danger" @dismissed="dismissCountDown=0" @dismiss-count-down="countDownChanged">
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
        name: "itemUpload",
        components: {navbar,},
        data() {
            return {
                hasImage: null,
                imageSrc: null,
                itemName: '',
                itemPrice: null,
                itemDetail : '',
                tagValue:null,
                dismissSecs: 5,
                dismissCountDown: 0,
                submitMsg: '',

            };
        },
        computed: {
        },
        watch: {

        },
        methods: {
            onPostItemBtnClick(event){
                event.preventDefault();
                if(this.itemName === '' || this.itemPrice === null){
                    // Check if item name and price is fulfilled
                    this.showAlertMsg("Please fill required information and try again. ")
                    return;
                }
                let token = localStorage.getItem('jwt');
                let submitImage = [];
                if(this.imageSrc !== null){
                    submitImage.push(this.imageSrc.substring(23));
                }
                this.itemPrice = parseFloat(this.itemPrice);
                //console.log(typeof this.itemPrice);

                let json = {
                    title: this.itemName,
                    NewPrice:this.itemPrice,
                    description: this.itemDetail,
                    tags: this.tagValue,
                    Images:submitImage,
                    Token: token,};
                //  Token: localStorage.getItem('jwt')}
                //console.log("JWT" + localStorage.getItem('jwt'));
                //console.log(JSON.stringify(json));
                this.sendItem(json);
            },
        sendItem(json) {
            // console.log(json)
            // this.$router.push({ path: "/browse" }).then(this.$forceUpdate());
            fetch('http://165.232.138.223:8080/item/upload', {
                method:"post",
                body: JSON.stringify(json),
                headers: {
                    'Content-Type': 'application/json'
                },
            }).then((data)=> {
                console.log(data);
                this.$router.push({ path: "/main" }).then(this.$forceUpdate());
            })
        },
            setImage: function(output) {
                this.hasImage = true;
                this.imageSrc = output;
                //console.log('Info', output);
                //console.log('Exif', output.exif);
            },
            countDownChanged(dismissCountDown) {
                this.dismissCountDown = dismissCountDown
            },
            showAlert() {
                this.dismissCountDown = this.dismissSecs
            },
            showAlertMsg(msg){
                this.submitMsg = msg;
                this.showAlert();
            }
        }
    };


</script>

<style >
    #fileInput {
        display: none;
    }
</style>