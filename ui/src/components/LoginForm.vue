<template>
    <div class="container">
      <div class="row justify-content-center mt-5">
        <div class="col-md-6">
          <div class="card">
            <div class="card-header">Login</div>
            <div class="card-body">
              <form @submit.prevent="login">
                <div class="mb-3">
                  <label for="email" class="form-label">Email address</label>
                  <input type="email" class="form-control" id="email" v-model="email" required>
                </div>
                <div class="mb-3">
                  <label for="password" class="form-label">Password</label>
                  <input type="password" class="form-control" id="password" v-model="password" required>
                </div>
                <button type="submit" class="btn btn-primary">Login</button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import AuthService from '../../AuthService';
  
  export default {
    data() {
      return {
        email: '',
        password: ''
      };
    },
    methods: {
        async login() {


      try {
        const { access_token, user } = await AuthService.login({
          email: this.email,
          password: this.password,
        });
        AuthService.setToken(access_token);
        AuthService.setUser(user);
        this.$router.push('/');
     
      } catch (error) {
        console.error(error);
      } finally {
        // empty state
      }
    },
},
  };
  </script>
  
  <style scoped>
  .container {
    margin-top: 100px;
  }
  .card {
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  .card-header {
    background-color: #f8f9fa;
    border-bottom: 1px solid #ccc;
  }
  .card-body {
    padding: 20px;
  }
  .btn-primary {
    width: 100%;
  }
  </style>
  