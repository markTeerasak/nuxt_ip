<template lang="html">
    <div>
        <v-container grid-list-xs>
            <v-form>
                <v-text-field v-model="username" label="username" variant="underlined"></v-text-field>
                <v-text-field v-model="password" label="password" variant="underlined" type="password"></v-text-field>
                <p class="text-red-darken-4">{{ errorMsg }}</p>
                <v-btn color="success" @click="handleLoginClicked">text</v-btn>
            </v-form>
        </v-container>
    </div>
</template>
<script>
import axios from 'axios';
import MD5 from "crypto-js/md5";
export default {
    layout: 'login',
    data() {
        return {
            username: '',
            password: '',
            url: '',
            errorMsg: ''
        }
    },
    methods: {
        handleLoginClicked() {   
            this.url = 'http://localhost/service/student/logins.php?username=' + this.username + '&password=' + MD5(this.password)
            axios.get(this.url).then((resp)=>{
                console.log(resp)
                localStorage.setItem('username', this.username)
                localStorage.setItem('password', MD5(this.password))
                window.location = '/user'
            })
            .catch(()=>{
                this.errorMsg = 'Incorrect username or password.'
            })
        }
    },
}
</script>
<style lang="css">
    
</style>