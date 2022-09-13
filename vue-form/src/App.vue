<template>
   <div>
    <ProgressBar></ProgressBar>
    <form v-on:submit.prevent="submitForm">
      <div>
        <label for="username">ID: </label>
        <input id="username" type="text" v-model="username"
        class="username-input"
        v-bind:class="{ 'error' : isError }">
      </div>
      <div>
        <label for="password">PW: </label>
        <input id="password" type="password" v-model="password">  
      </div>
      <button v-bind:disabled="!isUsernameValid" type="submit">로그인</button>
    </form>
    <p v-if="!isUsernameValid">이메일 형식이 아닙니다</p>
    <ToastPopup v-bind:open="isSuccess" v-on:close="isSuccess = false"></ToastPopup>
   </div>
</template>

<script>
import ToastPopup from '@/components/ToastPopup.vue';
import ProgressBar from '@/components/ProgressBar.vue';
const validateEmail = (email) => {
  return String(email)
    .toLowerCase()
    .match(
      /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
    );
};

export default {
    data() {
        return {
            username: "",
            password: "",
            isError: false,
            isSuccess: false
        };
    },
    computed: {
        isUsernameValid() {
            return validateEmail(this.username);
        }
    },
    methods: {
        submitForm() {
            this.isSuccess = true;
            // this.isError = true;
            this.initForm();
        },
        initForm() {
            this.username = "",
                this.password = "";
        }
    },
    components: { 
      ToastPopup,
      ProgressBar
    }
}
</script>

<style>
body {
  margin: 0;
}
form{
  padding: 5px 10px;
}
.username-input {
  outline: none;
}

.username-input.error{
  border: 1px solid red;
}
</style>