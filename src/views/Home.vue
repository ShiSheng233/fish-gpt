<template>
  <v-container class="h-full bg-slate-50">
    <div class="w-full h-full pb-28">
      <div v-for="(item, index) in messageList" :key="index">
        <div class="flex items-center my-4">
          <div>
            <v-avatar>
              <v-icon icon="mdi-account-circle"></v-icon>
            </v-avatar>
          </div>
          <div class="break-all whitespace-normal">
            {{ item.send }}
          </div>
        </div>
        <div>
          <v-banner :text="item.reply">
            <template #icon>
              <img class="avatar-image" src="https://avatars.githubusercontent.com/u/32504382" alt="avatar" />
            </template>
            <v-banner-actions>
              <v-btn icon="mdi-dots-vertical"></v-btn>
            </v-banner-actions>
          </v-banner>
        </div>
      </div>
    </div>
    <div class="fixed bottom-0 left-0 right-0 p-4 bg-white">
      <v-form ref="formRef">
        <div>
          <v-text-field
            variant="outlined"
            placeholder="Enter a prompt here"
            append-icon="mdi-send"
            v-model="model"
            :rules="[(v) => !!v || 'prompt is required']"
            @click:append="handleSend"
          ></v-text-field>
        </div>
      </v-form>
    </div>
  </v-container>
</template>

<script lang="ts" setup>
import { ref } from "vue";

interface Message {
  send: string;
  reply: string;
}

const model = ref("");
const formRef = ref();
const messageList = ref<Message[]>([]);

async function handleSend() {
  try {
    const { valid } = await formRef.value.validate();
    if (!valid) return;
    messageList.value.push({
      send: model.value,
      reply: Math.random() < 0.8 ? "你完蛋了。" : "草我",
    });
    model.value = "";
  } catch (error) {
    console.error(error);
  }
}
</script>

<style lang="scss" scoped>
.avatar-image {
  border-radius: 50%;
}
</style>
