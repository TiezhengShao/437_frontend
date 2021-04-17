<template>
  <body class="text-center">
    <b-container>
      <b-card
        title="Add a new item"
        img-src="https://picsum.photos/1600/600/?image=152"
        img-alt="Image"
        img-top
        tag="article"
        class="mb-2"
      >
          <!-- <b-form-group>
            <b-form-file
              v-model="file1"
              :state="Boolean(file1)"
              placeholder="Choose a file or drop it here..."
              drop-placeholder="Drop file here..."
            ></b-form-file>
            <div class="mt-3">Selected file: {{ file1 ? file1.name : "" }}</div>
          </b-form-group> -->
          <b-card-text>
              <b-form-input v-model="title" placeholder="Enter your name"></b-form-input>
              <div class="mt-2">Value: {{ title }}</div>
              <b-form-textarea
                id="textarea"
                v-model="text"
                placeholder="Enter item description and contact information"
                rows="3"
                max-rows="6"
                required
              ></b-form-textarea>

            <div class="mt-2">Value: {{ text }}</div>

            <b-button @click="onSubmit" type="submit" variant="primary">Submit</b-button>
          </b-card-text>
      </b-card>
    </b-container>
  </body>
</template>

<script>
export default {
  name: "newItem",
  data() {
    return {
    //   file1: null,
      text: "",
      title: ""
    };
  },
  methods: {
    onSubmit(event) {
      event.preventDefault();
      var token = localStorage.getItem('jwt');
      let json = {
          description: this.text,
          title: this.title,
          tags: ["all", Math.random().toString().substr(2, 8)],
          Token: token,};
        //   Token: localStorage.getItem('jwt')}
      console.log("JWT" + localStorage.getItem('jwt'));
      console.log(JSON.stringify(json));
      //this.sendItem(json);
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
            //this.$router.push({ path: "/browse" }).then(this.$forceUpdate());
         })
    }
  },
};
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
