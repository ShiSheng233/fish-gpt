<template>
  <div class="chat-box">
    <div class="title">Fish GPT</div>
    <div class="chat-history">
      <div v-for="(message, index) in messages" :key="index">
        <div class="message" :class="{ 'is-me': message.isMe }">
          <div class="avatar" v-if="!message.isMe">
            <img src="https://avatars.githubusercontent.com/u/32504382" alt="avatar" />
          </div>
          <div class="text">{{ message.text }}</div>
          <div class="tag" v-if="message.isMe">我</div>
        </div>
      </div>
    </div>
    <div class="chat-input">
      <el-input v-model="inputText" placeholder="请输入消息" @keyup.enter="sendMessage" />
    </div>
  </div>
</template>

<script>
document.title = 'Fish GPT';

import { ref } from 'vue';

export default {
  name: 'ChatBox',
  setup() {
    const messages = ref([]);
    const inputText = ref('');

    function sendMessage() {
      if (!inputText.value) {
        return;
      }
      const text = inputText.value;
      const reply = Math.random() < 0.8 ? '你完蛋了。' : '草我';
      messages.value.push({ text, isMe: true });
      messages.value.push({ text: reply, isMe: false });
      inputText.value = '';
    }

    return {
      messages,
      inputText,
      sendMessage,
    };
  },
};
</script>

<style scoped>
.chat-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  padding: 0 20px;
}

.title {
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 20px;
}

.chat-history {
  width: 100%;
  max-width: 600px;
  flex: 1;
  overflow-y: auto;
  padding: 20px;
}

.message {
  display: flex;
  align-items: center;
  padding: 10px 20px;
  margin-bottom: 10px;
  border-radius: 10px;
  position: relative;
}

.is-me {
  flex-direction: row-reverse;
  background: linear-gradient(to right, #00c6ff, #0072ff);
  color: #fff;
}

.avatar {
  width: 40px;
  height: 40px;
  margin-right: 10px;
  border-radius: 50%;
  overflow: hidden;
}

.avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.text {
  flex: 1;
}

.tag {
  position: absolute;
  top: -10px;
  left: -10px;
  width: 20px;
  height: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5px;
  background-color: #f0f0f0;
  font-size: 12px;
  font-weight: bold;
  color: #333;
}

.chat-input {
  width: 100%;
  max-width: 600px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
}

.el-input {
  flex: 1;
  margin-right: 20px;
}

</style>
