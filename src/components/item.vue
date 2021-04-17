<template>
<b-container>
  <body class="text-center">
  <b-card
    title=""
    tag="article"
    class="mb-2"
  >
    <b-img id="item-img" thumbnail fluid src="https://picsum.photos/450/250/?image=54" alt="Image 1"></b-img>
    <b-card-text>
      <h2 id="item-title">{{ title }}</h2>
      <p id="item-text">{{ text }}</p>
      <b-button @click="contactSeller" variant="outline-primary">Notify seller that you are interested</b-button>
    </b-card-text>

  </b-card>
</body>
</b-container>

</template>

<script>
    export default {
        name: "item",
        data() {
            return {
                title: 'Item not found',
                text: ''
            }
        },
        mounted() {
                this.fetchData();
                console.log("item mounted")
        },
        methods: {
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
                        this.title = data.items[0].Title
                        this.text = data.items[0].Description
                        console.log(data);
                    }).catch(error=>{
                        console.log(error);
                    }
                )
            },
            contactSeller() {
                // fetch('http://165.232.138.223:8080/item/upload', {
                //     method:"post",
                //     body: JSON.stringify({id: this.$route.params.id, })
                // }).then((response) => response.json()).then((data)=> {
                //     console.log(data);
                //     this.$router.push({ path: "/thanks" }).then(this.$forceUpdate());
                // })
                console.log({ id: this.$route.params.id });
                this.$router.push({ path: "/thanks" }).then(this.$forceUpdate())
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
