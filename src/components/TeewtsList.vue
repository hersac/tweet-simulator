<template>
    <div class="container">
        <h1 class="text-center mb-4">Lista</h1>
        <p v-if="tweets.length === 0">No hay tweets</p>
        <div class="tweet" v-for="(tweet, index) in tweets" :key="index">
            <p class="tweet__title">{{ tweet.username }}</p>
            <p class="tweet__text">{{ tweet.tweet }}</p>
            <span>{{ formatDate(tweet.createdAt) }}</span>
            <Close @click="deleteTeewt(tweet.id)"/>
        </div>
    </div>
</template>
<script>
import moment from 'moment';
import "moment/locale/es";
import { Close } from './Icons/index';
import { deleteTweetApi } from '../api/tweet';

export default {
    props:{
        tweets: Array,
        realoadTweets: Function,

    },
    components:{
        Close,
    },
    setup(props){
        const formatDate = (date)=>{
            return moment(date).fromNow();
        };

        const deleteTeewt = (idTweet)=>{
            deleteTweetApi(idTweet);
            props.realoadTweets();
        };

        return {
            formatDate,
            deleteTeewt,
        }
    }
    
}
</script>
<style lang="scss">
.tweet {
    position: relative;
    border: solid 1px #ccc;
    padding: 20px;
    margin-bottom: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    
    p {
        margin: 0;
    }

    &__title{
        position: absolute;
        top: -12px;
        left: 10px;
        background-color: #fff;
        padding: 0px 10px;
        font-weight: bold;
    }

    &__text {
        color: gray;
    }

    span {
        position: absolute;
        right: 10px;
        bottom: -9px;
        font-size: 12px;
        color: grey;
        background-color: #fff;
        padding: 0 20px;
        border: 1px solid #ccc;
    }
    svg {
        width: 20px;
        height: 20px;

        &:hover {
            cursor: pointer;
            color: red;
        }
    }
}


</style>