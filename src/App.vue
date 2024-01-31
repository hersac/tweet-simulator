<template>
  <div>
    <Menu :openCloseForm="openCloseForm" :showForm="showForm" />
    <TweetForm :showForm="showForm" :reloadTweets="reloadTweets" :openCloseForm="openCloseForm"/>
    <TweetsList :tweets="tweets" :realoadTweets="reloadTweets" />
  </div>
</template>

<script>
import { ref } from 'vue';
import Menu from './components/Menu.vue';
import TweetForm from './components/TweetForm.vue';
import TweetsList from './components/TeewtsList.vue';
import useFormTweet from './hooks/useFormTweet';
import { getTweetsApi } from './api/tweet';

export default {
  name: 'App',
  components: {
    Menu,
    TweetForm,
    TweetsList,
  },
  setup(){
    let tweets = ref(getTweetsApi().reverse());

    const reloadTweets = ()=>{
      tweets.value = getTweetsApi().reverse();
    };

    return {
      ...useFormTweet(),
      tweets, 
      reloadTweets,
    }
  }
}
</script>

<style lang="scss">

</style>
