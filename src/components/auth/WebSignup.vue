<template>
    <div class="container-fluid py-5" style="background-color: #f5f5f5">
      <div style="background-color: #ffffff" class="p-5 m-auto signup-form">
        <div class="text-center">
          <img src="../../assets/images/Vector.png" alt="Logo" />
          <h2 class="mt-4">Create your account</h2>
          <p>Enter your details to use all the app features.</p>
        </div>
        <form class="mt-3" @submit.prevent="register">
          <div class="row">
            <div class="col-md-6">
                <BaseInput type="text" label="Firstname" identity="inputFirstname" v-model="signupData.firstname"></BaseInput>
            </div>
            <div class="col-md-6">
              <BaseInput type="text" label="Lastname" identity="inputLastname" v-model="signupData.lastname"></BaseInput>
            </div>
          </div>
          <div class="my-4">
             <BaseInput type="text" label="Username" identity="inputUsername" v-model="signupData.username"></BaseInput>
          </div>
          <div class="my-4">
             <BaseInput type="text" label="Email" identity="inputEmail" v-model="signupData.email"></BaseInput>
          </div>
          <div class="my-4"> 
            <BaseInput type="password" label="Passoword" identity="inputPassword" v-model="signupData.password" @keyInput="passwordCheck"></BaseInput>
            <p class="text-danger mt-1 fw-medium" style="font-size: 11px" 
            :style="{ display: passwordStatusDisplay }">
              The password field must be at least 8 characters

            </p>
          </div>
          <div class="my-4">
             <BaseInput type="password" label="Confirm password" identity="inputConfirmPasswordn" v-model="signupData.confirmationPassword" @keyInput="confirmationPasswordCheck"></BaseInput>
             <p class="text-danger mt-1 fw-medium" style="font-size: 11px"
              :style="{ display: confirmPasswordDoesNotMacth }">
              The password confirmation does not match
            </p>
            <p class="text-success mt-1 fw-medium" style="font-size: 11px"
              :style="{ display: confirmPasswordMacth }">
              The password confirmation does match
            </p>
          </div>
          <div class="my-4">
             <BaseInput type="file"
                identity="recipeImage"
                label="Profile Photo"
                :isImage=true
                @input="checkImage">
            </BaseInput>
            <div class="border p-1 mt-2 rounded-circle">
              <img :src="signupData.imageLink" class="rounded-circle"
              width="140" height="150" style="object-fit: cover"/>
            </div>
          </div>
          <button type="submit">Register</button>
        </form>
        <div class="text-center mt-4">
          <p class="fw-semibold">
            Already have account?
            <span style="color: #4c4ddc">
              <router-link to="/login" class="text-decoration-none">Login</router-link>
              <!-- <a class="text-decoration-none" to="/login"> Login</a> -->
            </span>
          </p>
        </div>
      </div>
    </div>
</template>
  
<script setup>
import { reactive, ref } from "vue";
import BaseInput from "../ui/BaseInput.vue";
import { useStore } from "vuex";
import { useRouter } from "vue-router";

const signupData = reactive({
  firstname: "",
  lastname: "",
  username: "",
  email: "",
  password: "",
  confirmationPassword: "",
  isLogin: false,
  imageLink: "",

});

const passwordStatusDisplay = ref("none")

const passwordCheck = () => {

  if ( signupData.password.length < 8 ) {
    passwordStatusDisplay.value = "block"
  } else {
    passwordStatusDisplay.value = "none"
  }
}

const confirmPasswordDoesNotMacth = ref("none");
const confirmPasswordMacth = ref("none");
const confirmationPasswordCheck = () => {
if (signupData.confirmationPassword === "") {
confirmPasswordDoesNotMacth.value = "none";
confirmPasswordMacth.value = "none";
return;
}
if (signupData.password !== signupData.confirmationPassword) {
confirmPasswordDoesNotMacth.value = "block";
confirmPasswordMacth.value = "none";
return;
}
confirmPasswordDoesNotMacth.value = "none";
confirmPasswordMacth.value = "block";
};

const checkImage = (e) => {
  const file = e.target.files[0];
  const reader = new FileReader();
  reader.readAsDataURL(file);

  reader.addEventListener ("load", () => {
    signupData. imageLink = reader.result;
  });
};

const store = useStore()
const router = useRouter()
const register = async () => {
  if (
  signupData. password !== signupData.confirmationPassword ||
  signupData. password.length < 8
  ) {
  signupData. confirmationPassword = "";
  signupData. password = "";
  confirmPasswordDoesNotMacth. value = "none";
  confirmPasswordMacth. value = "none";
  }else {
  await store.dispatch("auth/getRegisterData" , signupData);
  router.push("/");
  }
  };
</script>