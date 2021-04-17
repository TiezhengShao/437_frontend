<template>
<b-container>
  <body class="text-center">
  <div>
  <b-card-group deck>
    <!-- <b-card title="Title" img-src="https://picsum.photos/300/300/?image=41" img-alt="Image" img-top>
      <b-card-text>
        This is a wider card with supporting text below as a natural lead-in to additional content.
        This content is a little bit longer.
      </b-card-text>
    </b-card> -->
    <b-card v-for="item in items" :key="item">
        <h3><a href="#" @click="makeItemLink(item.Tags[1])"> {{ item.Title }} </a></h3>
        <b-card-text>
            {{ item.Description }}
        </b-card-text>
    </b-card>
  </b-card-group>
</div>
</body>
</b-container>

</template>

<script>
    export default {
        name: "browse",
        data() {
            return {
                items: []
            }
        },
        mounted() {
                this.fetchData();
                console.log("browse mounted")
        },
        methods: {
            makeItemLink(id) {
                console.log(id);
                this.$router.push({ path: "/item/"+id }).then(this.$forceUpdate());
            },
            fetchData(){
                let json = {FuzzyTitle : ''};
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
                        this.items = data.Items;
                    }).catch(error=>{
                        console.log(error);
                    }
                )
            }
        }
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
        margin-bottom: -1px;
        border-bottom-right-radius: 0;
        border-bottom-left-radius: 0;
    }
    .form-signin input[type="password"] {
        margin-bottom: 10px;
        border-top-left-radius: 0;
        border-top-right-radius: 0;
    }

</style>