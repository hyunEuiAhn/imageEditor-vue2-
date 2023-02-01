<template>
  <div id="app">
    <img
      v-if="!openEditor"
      width="300"
      :src="src"
      @click="openEditor = true"
      alt="example image"
    />
    <VueFilerobotImageEditor
      v-if="openEditor"
      :src="src"
      :config="config"
      @complete="onComplete"
      @beforeComplete="onBeforeComplete"
      @close="onClose"
    />
  </div>
</template>

<script>
import VueFilerobotImageEditor, {
} from '@rotsen/vue-filerobot-image-editor'

export default {
  name: 'App',
  components: {
    VueFilerobotImageEditor
  },
  data () {
    return {
      openEditor: false,
      src: 'https://scaleflex.airstore.io/demo/stephen-walker-unsplash.jpg',
      config: {
        tools: ['crop', 'resize', 'shapes', 'text', 'pen'],
        finishButtonLabel: 'Save',
        annotationsCommon: {
          fill: '#ff0000'
        }
      }
    }
  },
  methods: {
    onComplete (file, object) {
      console.log('file' + file)
      this.openEditor = false
    },
    onBeforeComplete (element) {
      if (element && element.canvas) {
        this.src = element.canvas.toDataURL()
      }
      this.openEditor = false
    },
    onClose (status) {
      console.log(' close' + JSON.stringify(status, null, 3))
      this.openEditor = false
    }
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
