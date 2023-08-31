<template>
  <div>
    <input type="file" @change="uploadFile" accept="video/*" ref="file" />
    <button @click="submitFile">Upload!</button>
  </div>
</template>

<script lang="ts">
import { ref } from "vue";
import axios from "axios";

export default {
  setup() {
    const file = ref();

    const uploadFile = () => {
      console.log(file.value.files);
    };

    const submitFile = () => {
      var formData = new FormData();
      formData.append("file", file.value.files[0]);
      axios.post("http://localhost:8000/api/upload_video", formData, {
        headers: {
          "Content-Type": "multipart/form-data",
        },
      });
    };
    return { uploadFile, submitFile, file };
  },
};
</script>
