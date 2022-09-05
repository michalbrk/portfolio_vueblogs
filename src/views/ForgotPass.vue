<template>
    <div class="reset-password">
        <Modal v-if="iSmodalActive" :modalMessage="modalMessage" v-on:close-modal="closeModal"/>
        <Loading v-if="isLoading"/>
        <div class="form-wrap">
            <form class="reset">
                <p class="login-register">
                    Back to
                    <router-link class="router-link" :to="{ name: 'Login' }">Login</router-link>
                </p>
                <h2>Reset Password</h2>
                <p>Forgot your password? Enter your email to reset it</p>
                <div class="inputs">
                    <div class="input">
                        <input type="text" placeholder="Email" v-model="email">
                        <email class="icon"/>                        
                    </div>
                </div>
                <button @click.prevent="resetPass">Reset</button>
                <div class="angle"></div>
            </form>
            <div class="background"></div>
        </div>
    </div>
</template>
<script>
import email from "../assets/Icons/envelope-regular.svg";
import Modal from "../components/Modal.vue";
import Loading from "../components/Loading.vue";
import firebase from "firebase/app";
import "firebase/auth";

export default {
    name: "ForgotPass",
    components: { email, Modal, Loading },
    data() {
        return {
            email: "",
            iSmodalActive: false,
            modalMessage: "",
            isLoading: false
        }
    },
    methods: {
        resetPass() {
            this.isLoading = true;
            firebase
                .auth()
                .sendPasswordResetEmail(this.email)
                .then(() => {
                    this.modalMessage = "If your account exists, you will receive an email";
                    this.isLoading = false;
                    this.iSmodalActive = true;
                }).catch(err => {
                    this.modalMessage = err.message;
                    this.isLoading = false;
                    this.iSmodalActive = true;
                })
        },
        closeModal() {
            this.iSmodalActive = !this.iSmodalActive;
            this.email = ""; 
        }
    },
}
</script>
<style lang="scss" scoped>
.reset-password {
    position: relative;
    
    .form-wrap {

        .reset {

            h2 {
                margin-bottom: 8px;
            }

            p {
                text-align: center;
                margin-bottom: 32px;
            }
        }
    }
}
</style>