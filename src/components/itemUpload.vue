<template>
    <div>
        <navbar></navbar>

        <b-container>
            <!-- Stack the columns on mobile by making one full-width and the other half-width -->

            <b-row  class="pt-4">
                <b-col cols="12" md="8">
                    <b-container class="mt-3" >
                        <b-form @submit.stop.prevent="onSubmit">
                            <b-img  :src="imageSrc" class="mb-3" fluid-grow block rounded></b-img>

                            <div class="d-flex mb-3">
                                <b-form-file v-model="image" placeholder="Choose an image" class="w-auto flex-grow-1"></b-form-file>

                                <b-button v-if="hasImage" variant="danger" class="ml-3" @click="clearImage">Clear image</b-button>
                            </div>




<!--                            <b-button :disabled="!hasImage" variant="primary" type="submit">Upload image</b-button>-->
                        </b-form>
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

                        <b-button variant="success" class="btn-lg btn-block" @click="onPostItemBtnClick()" type="submit">Publish</b-button>

                    </form>

                </b-col>
            </b-row>


        </b-container>

    </div>

</template>

<script>
    import navbar from "@/components/navbar";

    const base64Encode = data =>
        new Promise((resolve, reject) => {
            const reader = new FileReader();
            reader.readAsDataURL(data);
            reader.onload = () => resolve(reader.result);
            reader.onerror = error => reject(error);
        });

    export default {
        name: "itemUpload",
        components: {navbar,},
        data() {
            return {
                image: null,
                imageSrc: null,
                itemDetail : null,
                itemName: null,
                itemPrice:null,
                tagValue:null,

            };
        },
        computed: {
            hasImage() {
                return !!this.image;
            }
        },
        watch: {
            image(newValue, oldValue) {
                console.log(newValue.size);
                if (newValue !== oldValue) {
                    if (newValue) {
                        base64Encode(newValue)
                            .then(value => {
                                this.imageSrc = value;
                            })
                            .catch(() => {
                                this.imageSrc = null;
                            });
                    } else {
                        this.imageSrc = null;
                    }
                }
            }
        },
        methods: {
            clearImage() {
                this.image = null;
            },

            onSubmit() {
                if (!this.image) {
                    alert("Please select an image.");
                    return;
                }

                alert("Form submitted!");
            }
        }
    };


</script>

<style scoped>

</style>