<script setup lang="ts">
import { isPermissionGranted, requestPermission, sendNotification} from '@tauri-apps/api/notification';
import { arch, platform, tempdir, type, version } from '@tauri-apps/api/os';
import { message } from '@tauri-apps/api/dialog';


async function send_notification() {
  if (await requestPermission() === 'granted') {
    sendNotification({
      title: "小土坡信息提示",
      body: "message body"
    });
  }
}

// 获取 Arch 信息
async function getArchInfo() {
  const result = await arch() as string;
  await message(`Arch: ${result}`, {title: "Arch Info"});
}

// 获取 PlatformInfo 信息
async function getPlatformInfo() {
  const result = await platform() as string;
  await message(`Platform: ${result}`, {title: "Platform Info"});
}

// 获取系统 temp 路径信息
async function getTempDirInfo() {
  const result = await tempdir();
  await message(`temp dir: ${result}`, {title: "Temp Dir Info"});
}

// 获取 OS 类型
async function getOSTypeInfo() {
  const result = await type() as string;
  await message(`OS type: ${result}`, {title: "OS Type Info"});
}

// 获取 OS 版本
async function getOSVersionInfo() {
  const result = await version();
  await message(`OS Version: ${result}`, {title: "OS Version Info"});
}
</script>

<template>
  <div class="container">
    <h1>Welcome to Tauri!</h1>
    <div class="mb-3">
      <button type="button" class="btn btn-primary me-1 mb-1" @click="send_notification">发送通知</button>
      <button type="button" class="btn btn-primary me-1 mb-1" @click="getArchInfo">显示Arch信息</button>
      <button type="button" class="btn btn-primary me-1 mb-1" @click="getPlatformInfo">显示Platform信息</button>
      <button type="button" class="btn btn-primary me-1 mb-1" @click="getTempDirInfo">显示TempDir信息</button>
      <button type="button" class="btn btn-primary me-1 mb-1" @click="getOSTypeInfo">显示OS Type信息</button>
      <button type="button" class="btn btn-primary me-1 mb-1" @click="getOSVersionInfo">显示OS Version信息</button>
    </div>
  </div>
</template>

<style scoped>
.test {
  background: white;
}
</style>
