<script setup lang="ts">
import { ref } from "vue";
import liff from "@line/liff";

const name = ref();
const storeID = ref<string>("");
liff
  .init({ liffId: "2000282081-MblO1kW3" })
  .then(() => {
    if (liff.isInClient())
      liff.getProfile().then((profile) => {
        name.value = profile.displayName;
      });
    /*
    console.log("初始化成功");
    if (liff.isLoggedIn()) {
      console.log("已登入");
      getProfile();
    } else {
      console.log("未登入");
      liff.login();
    }
    */
  })
  .catch(() => {
    console.log("初始化失敗");
  });

const closeIntergrate = () => {
  if (!liff.isInClient()) {
    window.alert("目前外部瀏覽器上不支援此功能");
  } else {
    liff
      .sendMessages([
        {
          type: "text",
          text: "關閉_" + storeID.value,
        },
      ])
      .then(() => {
        window.alert(
          "關閉_" + storeID.value + " 訊息已傳送，請至聊天室確認結果"
        );
        liff.closeWindow();
      })
      .catch((error) => {
        window.alert("Error sending message: " + error);
      });
  }
};

const openIntergrate = () => {
  if (!liff.isInClient()) {
    window.alert("目前外部瀏覽器上不支援此功能");
  } else {
    liff
      .sendMessages([
        {
          type: "text",
          text: "開啟_" + storeID.value,
        },
      ])
      .then(() => {
        window.alert(
          "開啟_" + storeID.value + " 訊息已傳送，請至聊天室確認結果"
        );
        liff.closeWindow();
      })
      .catch((error) => {
        window.alert("Error sending message: " + error);
      });
  }
};
</script>

<template>
  <div
    class="flex items-center justify-start w-[100%] h-[100vh] bg-slate-200 flex-col"
  >
    <div class="mt-10">
      <div class="flex justify-center w-[100%] rounded-full mt-20">
        <img class="w-28 h-28 rounded-full" src="/robot.png" />
      </div>

      <div class="flex justify-center w-[100%] flex-row my-4">
        Hello, {{ name }}
      </div>
      <div class="flex justify-center w-[100%] flex-row mb-4">
        歡迎使用LineBot串接UberEats功能
      </div>
      <div class="p-4">
        <div class="flex items-center justify-center w-[100%] flex-row mb-8">
          <div class="mr-4">storeID:</div>
          <input v-model="storeID" class="rounded-xl p-2 shadow-md" />
        </div>
        <div class="grid grid-cols-8 gap-4">
          <div
            class="w-full col-span-4 flex justify-center bg-slate-300 p-4 rounded-full hover:bg-slate-500 shadow-md"
            @click="closeIntergrate"
          >
            關閉UberEats
          </div>
          <div
            class="w-full col-span-4 flex justify-center bg-slate-300 p-4 rounded-full hover:bg-slate-500 shadow-md"
            @click="openIntergrate"
          >
            開啟UberEats
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
