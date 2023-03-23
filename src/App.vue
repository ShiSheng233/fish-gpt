<template>
  <div class="chat-box">
    <div class="title">Fish GPT</div>
    <div class="chat-history">
      <div v-for="(message, index) in messages" :key="index">
        <div class="message" :class="{ 'is-me': message.isMe }">
          <div class="avatar" v-if="!message.isMe">
            <img src="https://avatars.githubusercontent.com/u/32504382" alt="avatar" />
          </div>
          <div class="message-content">
            <div class="text">{{ message.text }}</div>
            <div class="timestamp">{{ message.timestamp }}</div>
            <div class="tag" v-if="message.isMe">我</div>
          </div>
        </div>
      </div>
    </div>
    <div class="chat-input">
      <el-input v-model="inputText" placeholder="请输入消息..." @keyup.enter="sendMessage" />
      <el-button class="send-button" type="primary" @click="sendMessage">发送</el-button>
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
      const timestamp = new Date().toLocaleTimeString();
      messages.value.push({ text, isMe: true, timestamp });
      messages.value.push({ text: reply, isMe: false, timestamp });
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
  padding: 10px;
  background-color: #f0f0f0;
}

.title {
  font-size: 20px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 10px;
}

.chat-history {
  width: 100%;
  max-width: 600px;
  flex: 1;
  overflow-y: auto;
  padding: 10px;
}

.message {
  display: flex;
  align-items: flex-start;
  margin-bottom: 10px;
  border-radius: 10px;
  position: relative;
}

.message-content {
  display: flex;
  flex-direction: column;
  margin-left: 10px;
  max-width: 80%;
}

.is-me .message-content {
  align-items: flex-end;
}

.text {
  font-size: 14px;
  color: #333;
  margin-bottom: 5px;
}

.timestamp {
  font-size: 12px;
  color: gray;
  margin-bottom: 5px;
}

.tag {
  font-size: 12px;
  font-weight: bold;
  color: white;
  background-color: #0072ff;
  padding: 2px 5px;
  border-radius: 5px;
}

.avatar {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  overflow: hidden;
}

.avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.chat-input {
  width: 100%;
  max-width: 600px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #fff;
  border-radius: 5px;
}

.el-input {
  flex: 1;
  margin-right: 10px;
  font-size: 14px;
}

.send-button {
  width: 60px;
  height: 30px;
  border-radius: 5px;
  background-color: #0072ff;
  color: white;
  font-size: 14px;
}
</style>
