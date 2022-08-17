<template>
  <div class="app">
    <button v-on:click="postTweet">ツイート</button>
    <!-- 変更点１ -->
    <div>
      <p v-for="tweet in tweets" :key="tweet.id">
        {{ tweet.text }}
      </p>
    </div>
  </div>
</template>

<script>
/* 変更点１ */
import { collection, addDoc, getDocs } from "firebase/firestore";
import { db } from "./firebase";

export default {
  data() {
    return {
      /* 変更点２ */
      tweets: [
        // {
        //   id: "0GwoGZuhTNhqHQDBeiVW",
        //   text: "こんにちは、ツイートの本文です。"
        // }
      ],
    };
  },
  methods: {
    postTweet() {
      const tweet = {
        text: "this is the tweet",
      };
      addDoc(collection(db, "tweets"), tweet).then((ref) => {
        this.tweets.push({
          id: ref.id,
          ...tweet,
        });
      });
    },
  },
};
</script>
