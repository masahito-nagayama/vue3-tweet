<script setup lang="ts">
import { ref } from 'vue'
const tweets = ref([{ id: 0, description: '頑張れ'}, {　id: 1, description: 'おまえががんばれ'}])
const inputtingDescription = ref<string>('')
const postTweet = () => {
  const tweet = { id: Math.random(), description: inputtingDescription.value }
  tweets.value.push(tweet)
}

const deleteTweet = (id:　number) => {
  tweets.value = tweets.value.filter(t => t.id !== id)
  // 押されたtweet.id以外のオブジェクトを配列に格納していることで削除されたように表現している。
}

</script>

<template>
  <div class="container">
    <h1>Tweeter</h1>
    <div class="form-container">
      <input v-model="inputtingDescription"/>
      <button class="save-button" @click="postTweet()">post</button>
    </div>
    <div>
      <div class="tweet-container">
        <p v-if="tweets.length <= 0">現在Tweeetはなにもありません。</p>
        <ul>
          <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
            <span>{{ tweet.description }}</span>
            <button @click="deleteTweet(tweet.id)" class="delete-button">Delete</button>
          </li>
        </ul>
      </div> 
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: aliceblue;
  padding: 24px 0;
  width: 60%;
  margin-bottom: 12px;
  border-radius: 4px;
}

.tweet-list {
  list-style: none;
  margin-bottom: 12px;
  font-size: 20px;
  display: flex;
  justify-content: space-between;
  background-color: rgb(83, 166, 240);
  border-radius: 4px;
  padding: 8px 20px;
  width: 500px;
}

.save-button {
  color: #fff;
  font-weight: bold;
  background-color: #68c9c9;
  border-radius: 2px;
  border: none;
  width: 60px;
  height: 22px;
}

.delete-button {
  color: #fff;
  font-weight: bold;
  background-color: #f11708;
  border-radius: 2px;
  border: none;
  width: 60px;
  height: 22px;
}

.save-button:hover {
  background-color: #37bdbd;
}
.delete-button:hover {
  background-color: #f5746f;
}

input {
  margin-bottom: 16px;
}

label {
  font-size: 20px;
  font-weight: bold;
}
</style>