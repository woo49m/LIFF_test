<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
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
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
