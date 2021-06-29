<template>
  <div id="app">
    <div class="btn-container">
      <FileUploaderConstructor
          v-bind="{
              multiple: true,
              drop: true,
              dropDirectory: true,
              fileDrop: true,
              lengthText: 15,
              showOnlyFiles: true
            }"
          @changeFile="uploadFiles"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import FileUploaderConstructor from "./components/FileUploaderConstructor";
export default {
  name: 'App',
  components: {FileUploaderConstructor},
  data() {
    return {
      file: []
    }
  },
  methods: {
    uploadFiles(files) {
      let formData = new FormData();
      for(let i in files) {
        formData.append('file', files[i].file);
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
      this.$root.$emit('clearUploaderConstructor')
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


input[type="file"] {
  display: none;
}


</style>
