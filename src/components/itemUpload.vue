<template>
    <div>
        <navbar></navbar>

        <b-container>
            <!-- Stack the columns on mobile by making one full-width and the other half-width -->
            <b-row  class="pt-4">
                <b-col cols="12" md="8">
                    <b-img src="https://picsum.photos/300/150/?image=41" rounded="" fluid-grow alt="Fluid-grow image"></b-img>


                </b-col>
                <b-col cols="6" md="4" >
                    <form class="form-item-post"  >
                        <b-form-input id="input-2" v-model="itemName" type="text" placeholder="Item Name" class="mb-2" required></b-form-input>

                        <b-input-group prepend="$" class="mb-2" >
                            <b-form-input id="item-price" v-model="itemPrice" placeholder="123.45" type="number" required></b-form-input>
                        </b-input-group>

                        <div class="mb-2">
                            <b-form-tags input-id="tags-basic" v-model="tagValue"></b-form-tags>
                        </div>

                        <b-button variant="secondary" class="btn-lg btn-block" @click="onPostItemBtnClick()" type="submit">List my item now</b-button>

                    </form>

                </b-col>
            </b-row>


        </b-container>
    </div>

</template>

<script>
    import navbar from "@/components/navbar";
    export default {
        name: "itemUpload",
        components: {navbar}
    }
</script>

<style scoped>

</style>