<template>
  <div id="app">
    <div class="btn-container">
      <label class="upload-btn"> Upload
        <input type="file" id="file"  ref="file" @change="handleFileUpload()"/>
      </label>
<!--      <FileUploaderConstructor-->
<!--          v-bind="{-->
<!--              multiple: true,-->
<!--              drop: true,-->
<!--              dropDirectory: true,-->
<!--              fileDrop: true,-->
<!--              lengthText: 15,-->
<!--              showOnlyFiles: true-->
<!--            }"-->
<!--          @changeFile="check"-->
<!--      />-->
    </div>
  </div>
</template>

<script>
import axios from 'axios'
// import FileUploaderConstructor from "./components/FileUploaderConstructor";
export default {
  name: 'App',
  // components: {FileUploaderConstructor},
  data() {
    return {
      file: ''
    }
  },
  methods: {
    handleFileUpload(){
      this.file = this.$refs.file.files[0];
      console.log(this.file)
      this.uploadFile()
    },
    // check(file){
    //   this.uploadFile(file)
    //   console.log(file, 'check')
    // },

    uploadFile() {
      let formData = new FormData();
      formData.append('file', this.file);
      console.log(formData, 'formData')
      axios({
        url: 'http://localhost:8080',
        method: 'POST',
        data: formData
      })
          .then((response) => {
            console.log(response)
          })
          .catch((error) => console.log(error))
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  height: 100%;

}
.btn-container {
  height: 800px;
  width: 30%;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.upload-btn {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #66CB9F;
  padding: 20px 30px;
  border: none;
  border-radius: 10px;
  color: #fff;
  font-size: 24px;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.1s ease-in;
  margin: 0 20px;
}
.upload-btn:active {
  background-color: #4AAE8C;
}

input[type="file"] {
  display: none;
}


</style>
