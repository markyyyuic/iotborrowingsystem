<template>
    <div class="background-login"></div>

    <h1>Open <br>Laborotary <br>Borrowing <br>System</h1>

    <div class="login-bar">
        <img src="../assets/loginlogo.png" alt="">
        <form @submit.prevent="attemptLogin">
            
            <div class="username">
                <i class='bx bxs-user-circle'></i>
                <input v-model="admin_User" type="text" id="admin_User" name="admin_User" placeholder="enter username">
            </div>

            <div class="password">
                <i class='bx bx-lock-alt' ></i>
                <input v-model="admin_Password" type="password" id="admin_Password" name="admin_Password" placeholder="enter password">
            </div>
          
           <a href="">Forgot Password?</a>
           <button class="login">Login</button>

        </form>
    </div>

</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      admin_User: '',
      admin_Password: ''
    };
  },
  methods: {
    attemptLogin() {
      const formData = new FormData();
      formData.append('admin_User', this.admin_User);
      formData.append('admin_Password', this.admin_Password);

      axios.post('http://127.0.0.1:8000/api/administrator/login/', formData)
        .then(response => {
          if (response.data) {
            console.log("Success");
            this.$router.push('/maindashboards');
          } else { 
            console.log("Error")
          }
        })
        .catch(error => {
          console.error("Error:", error);
        });
    }
  }
};

</script>


<style scoped>

html, body {
  height: 100%;
  width: 100%;
  margin: 0;
  overflow: hidden;
  
}

.background-login {
  position: fixed;
  top: 0;
  left: 0;
  width: 80%;
  height: 100%;
  z-index: -1;
  overflow: hidden;
  transform: scaleX(-1);
  background-image: linear-gradient(to left, rgba(232, 22, 82, .8) 5%, rgba(255, 203, 213, 0.1) 75%), url('../assets/bg.jpg');
  background-size: cover;
  background-position: center;
  background-size: cover; 
  
}

.login-bar {
    width: 28%;
    height: 100vh;
    position: fixed;
    right: 0px;
    top: 0px;
    background-color: #FFF;
    box-shadow: 3px 5px  rgba(0, 0, 0, 0, 0.1);

}

h1 {
    position: fixed;
    bottom: 30%;
    font-size: 80px;
    font-family: 'Roboto', sans-serif;
    font-weight: bold;
    left: 5%;
    color: #FFF;
}



.login-bar form {
    padding: 5px 30px 20px 30px;
}

.username, .password {
    width: 75%;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    border: none;
    border-bottom: 1px solid;
    margin-left: 15%;
    margin-top: 4%;

}

.username input, .password input {
    width: 100%;
    height: 100%;
    border: none;
    outline: none;

    
    

}

.username i, .password i {
    height: 40px;
    width: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 1px solid #acacac;
    color: #555;
   

}

.login-bar img {
    position: relative;
    left: 25%;
    margin-top: 15%;
    margin-bottom: 23%;
    
}

.login-bar a {
    position: fixed;
    margin-top: 4%;
    color: #E81652;
    font-size: 15px;
    margin-left: 2%;
    font-family: 'Roboto', sans-serif;
}

.login-bar .login {
    position: fixed;
    margin-top: 50px;
    width: 10%;
    height: 45px;
    background: #E81652;
    border: 1px;
    border-style: solid;
    outline: none;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, .2);
    cursor: pointer;
    font-size: 16px;
    color: #ffffff;
    font-weight: 600;
    margin-left: 13%;
}

.login:hover {
    background: #FFF;
    color: black;
}




</style>