<template>
    <div class="twwet-form container" :class="{open: showForm}" >
        <form @submit.prevent="sendTweet">
            <input type="text" class="form-control" placeholder="Nombre" v-model="username"/>
            <textarea rows="3" class="form-control" placeholder="Escribe el tweet..." v-model="tweet"></textarea>
            <button type="submit" class="btn btn-primary">Enviar Tweet</button>
        </form>
    </div>
</template>
<script>
import { ref } from 'vue';
import { saveTweetApi } from '../api/tweet';
export default {
    props:{
        showForm: Boolean,
        reloadTweets: Function,
        openCloseForm: Function,
    },
    setup(props){
        let username = ref('');
        let tweet = ref('');

        const sendTweet = ()=>{
            if(!tweet.value || !username.value) return;

            saveTweetApi(tweet.value, username.value);
            tweet.value = "";
            username.value = "";
            props.reloadTweets();
            props.openCloseForm();
        };

        return {
            username,
            tweet,
            sendTweet,
        }
    }
}
</script>
<style lang="scss" scope>
    .twwet-form {
        margin-top: 20px;
        height: 0;
        overflow: hidden;

        &.open {
            height: auto;
        }
    }

    form {
        margin-bottom: 50px;
        input {
            margin-bottom: 10px;
        }

        button {
            width: 100%;
            margin-top: 10px;
        }
    }
</style>