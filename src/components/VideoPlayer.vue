<template>
  <div class="videoplayer">
    <aside class="video">
      <video
        id="VideoPlayer"
        ref="videoplayer"
        tabindex="-1"
        :src="vid_src"
        controls
      ></video>
    </aside>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import { desktopDir } from "@tauri-apps/api/path";
import { convertFileSrc } from '@tauri-apps/api/tauri';


const vid_src = ref("");
onMounted(async () => {
  const dir = await desktopDir();
  vid_src.value = convertFileSrc(`${dir}vid_test.mp4`);
});
</script>

<style scoped lang="scss">
$width: 350px;
div.videoplayer {
  display: flex;
  flex-direction: column;
  > aside {
    flex: 0 1 100%;
  }
}
aside.controls,
aside.buttons {
  height: 30px;
}
aside.controls {
  width: 100%;
  progress,
  input {
    width: 100%;
  }
}
aside.video {
  height: calc(600px / 1.77);
  video {
    width: 100%;
    height: 100%;
    border: 1px solid #000;
    background-color: #000;
    outline: none !important;
    box-shadow: none !important;
  }
}
</style>
