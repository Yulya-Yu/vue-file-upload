<template>
  <div class="background-uploader">
    <div
        v-if="$refs.uploadConstructor && $refs.uploadConstructor.dropActive && fileDrop"
        class="drop-active"
    >
    </div>
    <div class="files-background">
      <file-upload
          input-id="uploadConstructor"
          class="file-uploader"
          post-action="/upload/post"
          :multiple="multiple"
          :drop="drop"
          :drop-directory="dropDirectory"
          v-model="file"
          ref="uploadConstructor"
          v-if="showOnlyFiles"
      >
        <div class="file-description">Drop or choose</div>
      </file-upload>
    </div>
  </div>
</template>

<script>
import FileUpload from 'vue-upload-component'

export default {
  name: 'FileUploaderConstructor',
  mixins: [],
  props: [
    'multiple',
    'drop',
    'dropDirectory',
    'fileDrop',
    'deep',
    'lengthText',
    'showOnlyFiles',
    'editingFiles'
  ],
  components: {FileUpload},
  data() {
    return {
      file: []
    }
  },
  mounted() {
    this.$root.$on('clearUploaderConstructor', () => {
      this.file.length = 0
    })
  },
  methods: {},
  computed: {},
  watch: {
    file() {
      this.$emit('changeFile', this.file)
    }
  },
  validations: {},
  directives: {}
}
</script>

<style scoped>
.files-background {
  position: relative;
  z-index: 99;
  margin-top: 20px;
}

.file-uploader {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 295px;
  height: 170px;
  border: 1px dashed #a5a5a5;
  border-radius: 10px;
}
/deep/.file-label {
  display: flex;
  align-items: center;


}
/deep/img {
  margin-right: 6px;
}

/deep/div {
  font-style: normal;
  font-weight: normal;
  font-size: 24px;
  line-height: 16px;
  color: #1284ff;
}
/deep/.file-description {
  margin-top: 6px;
  font-style: normal;
  font-weight: 500;
  font-size: 24px;
  line-height: 14px;
  color: #c1c1c1;
}

/deep/label {
  cursor: pointer;
}
</style>
