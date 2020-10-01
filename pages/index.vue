<template>
  <div class="container">
    <div>
      <h1 class="title">
        nuxt-toast-ui-poc
      </h1>
      <div class="main">
        <h2>Editor by tui.editor vue-editor component</h2>
        <EditorPlain></EditorPlain>

        <h2>Editor by tui.editor vue-editor component</h2>
        <EditorVue></EditorVue>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'
import EditorPlain from '~/components/EditorPlain.vue'
import EditorVue from '~/components/EditorVue.vue'

export default defineComponent({
  components: {
    EditorPlain,
    EditorVue
  },
  setup () {

  }
})
</script>
<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

h2 {
  font-size: 24px;
}

</style>
