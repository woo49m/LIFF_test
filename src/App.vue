<script setup lang="ts">
import { ref } from "vue";
import liff from "@line/liff";

const name = ref();
const storeID = ref<string>("");
liff
  .init({ liffId: "2000282081-MblO1kW3" })
  .then(() => {
    console.log("初始化成功");
    if (liff.isLoggedIn()) {
      getProfile();
    } else {
      liff.login();
    }
  })
  .catch(() => {
    console.log("初始化失敗");
  });

const getProfile = () => {
  liff.getProfile().then((profile) => {
    name.value = profile.displayName;
  });
};
getProfile();

const closeIntergrate = () => {
  if (!liff.isInClient()) {
    window.alert(
      "This button is unavailable as LIFF is currently being opened in an external browser."
    );
  } else {
    liff
      .sendMessages([
        {
          type: "text",
          text: "關閉_" + storeID.value,
        },
      ])
      .then(() => {
        window.alert("Message sent");
        liff.closeWindow();
      })
      .catch((error) => {
        window.alert("Error sending message: " + error);
      });
  }
};

const openIntergrate = () => {
  if (!liff.isInClient()) {
    window.alert(
      "This button is unavailable as LIFF is currently being opened in an external browser."
    );
  } else {
    liff
      .sendMessages([
        {
          type: "text",
          text: "開啟_" + storeID.value,
        },
      ])
      .then(() => {
        window.alert("Message sent");
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
          <input v-model="storeID" class="rounded-xl p-2" />
        </div>
        <div class="grid grid-cols-8 gap-4">
          <div
            class="w-full col-span-4 flex justify-center bg-slate-300 p-4 rounded-full hover:bg-slate-500"
            @click="closeIntergrate"
          >
            關閉UberEats
          </div>
          <div
            class="w-full col-span-4 flex justify-center bg-slate-300 p-4 rounded-full hover:bg-slate-500"
            @click="openIntergrate"
          >
            開啟UberEats
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
