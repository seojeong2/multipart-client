<template>
  <div class="information">
    <p>파일 업로드</p>
    <input type="file" @change="selectFile" ref="imgFile" />
    <button @click="submit">서버에 전송하기</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      files: [],
      image: "test_image",
    };
  },
  methods: {
    async submit() {
      const formData = new FormData();
      formData.append("image", this.image);

      // try {
      //   const { data } = await axios.post(
      //     "http://localhost:8085/upload",
      //     formData,
      //     {
      //       headers: {
      //         "Content-Type": "multipart/form-data",
      //       },
      //     }
      //   );
      //   console.log(data);
      // } catch (err) {
      //   console.log(err);
      // }
      axios
        .post("/upload", formData, {
          headers: {
            "Content-Type": `multipart/form-data;`,
          },
          baseURL: "http://localhost:8085",
        })
        .then((response) => {
          console.log("success");

          alert("등록되었습니다!");
        })
        .catch((error) => {
          console.log("error");
        });
    },
    selectFile(event) {
      this.image = this.$refs.imgFile.files[0];
    },
  },
};
</script>
