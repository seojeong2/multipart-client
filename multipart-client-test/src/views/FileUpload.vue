<template>
  <div class="information">
    <p>파일 업로드</p>
    <button @click="$refs.fileRef.click">선택</button>
    <input type="file" @change="selectFile" multiple ref="fileRef" hidden />
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      files: [],
      backendUrl: "http://localhost:8080",
    };
  },
  methods: {
    async fetchFiles() {},
    selectFile(event) {
      const formData = new FormData();

      for (const file of event.target.files) {
        formData.append("files", file);
      }
      axios
        .post(`${this.backendUrl}/files`, formData, {
          headers: { "Content-Type": "multipart/form-data" },
        })
        .then(() => {
          //this.fetchFiles();
        })
        .catch((error) => {
          alert(error.message);
        });
    },
  },
};
</script>
