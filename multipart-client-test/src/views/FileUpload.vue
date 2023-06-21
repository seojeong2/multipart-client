<template>
  <div class="information">
    <p>파일 업로드</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      files: [],
      backendUrl: "http://localhost:8080",
      image: "test_image",
    };
  },
  methods: {
    async submit() {
      const formData = new FormData();
      formData.append("image", this.image);

      try {
        const { data } = await axios.post(
          "http://localhost:8085/upload",
          formData,
          {
            headers: {
              "Content-Type": "multipart/form-data",
            },
          }
        );
        console.log(data);
      } catch (err) {
        console.log(err);
      }
    },
    selectFile(file) {
      this.image = file;
    },
  },
};
</script>
