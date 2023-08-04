<script setup lang="ts">
import { ref } from "vue";
import liff from "@line/liff";

liff
  .init({ liffId: "2000282081-MblO1kW3" })
  .then(() => {
    console.log("初始化成功");
    let os = liff.getOS();
    var lineVersion = liff.getLineVersion();
    console.log(lineVersion);
    console.log(os);
    if (liff.isApiAvailable("shareTargetPicker")) {
      //todo
    } else {
      alert("你的 LINE App 暫時不支援 Share Target Picker");
    }
    var isInClient = liff.isInClient();
    console.log("isInClient", isInClient);
    if (!liff.isLoggedIn()) {
      console.log("你還沒登入Line哦！");
      liff.login();
    } else {
      console.log("你已經登入Line哦！");
    }
  })
  .catch(() => {
    console.log("初始化失敗");
  });
const name = ref();

const getProfile = () => {
  liff.getProfile().then((profile) => {
    name.value = profile;
  });
};

const sendMessage = () => {
  if (!liff.isInClient()) {
    window.alert(
      "This button is unavailable as LIFF is currently being opened in an external browser."
    );
  } else {
    liff
      .sendMessages([
        {
          type: "text",
          text: "Hello, World!",
        },
      ])
      .then(() => {
        window.alert("Message sent");
      })
      .catch((error) => {
        window.alert("Error sending message: " + error);
      });
  }
};
</script>

<template>
  <div>
    功能測試
    <div>
      <button @click="getProfile">獲得用戶資訊</button>
      <div>{{ name }}</div>
    </div>
    <button @click="sendMessage">回傳訊息</button>
  </div>
</template>
