<template>
  <div class="container">
    <div class="row justify-content-center" id="logincontainer">
      <div class="col-md-8">
        <div class="card" id="cardregister">
          <div class="card-body">
            <div v-if="error" class="alert alert-danger">{{error}}</div>
            <form action="#" @submit.prevent="submit">
              <div class="form-group row m-2">
                <label for="email" class="col-md-4 col-form-label text-md-right">Email:</label>

                <div class="col-md-6">
                  <input
                    id="email"
                    type="email"
                    class="form-control"
                    name="email"
                    value
                    required
                    autofocus
                    v-model="form.email"
                  />
                </div>
              </div>

              <div class="form-group row m-2">
                <label for="password" class="col-md-4 col-form-label text-md-right">Password:</label>

                <div class="col-md-6">
                  <input
                    id="password"
                    type="password"
                    class="form-control"
                    name="password"
                    required
                    v-model="form.password"
                  />
                </div>
              </div>
              <br>
              <div class="form-group row mb-0">
                <div class="col-md-12">
                  <b-button type="submit" class="btn" squared id="loginbutton">Login</b-button>
                </div>
              </div>
              <br>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable*/
import firebase from "firebase";

export default {
  data() {
    return {
      form: {
        email: "",
        password: ""
      },
      error: null
    };
  },
  methods: {
    submit() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.form.email, this.form.password)
        .then(data => {
          this.$router.push({name: 'Home',})
        })
        .catch(err => {
          this.error = err.message;
        });
    }
  }
};
</script>

<style scoped>
  #logincontainer{
    margin: 10%;
  }

  #cardregister{
    box-shadow: 5px 5px 5px 1px darkslateblue;
  }

  #loginbutton{
    background-color:white;
    color:darkslateblue;
    border: 1px solid darkslateblue;
    padding-left: 5%;
    padding-right: 5%;
  }

  #loginbutton:hover{
    background-color:darkslateblue;
    color:white;
    border: 1px solid darkslateblue;
  }
</style>