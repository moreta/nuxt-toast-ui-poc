<template>
  <div class="container">
    <div>
      <h1 class="title">
        nuxt-toast-ui-poc
      </h1>
      <div class="main">
        <ClientOnly placeholder="Loading...">
          <div
            id="editor"
            ref="editorEl"
          ></div>
          <div>
            <button @click="handleClick">
              result
            </button>
            <div>{{ htmlResult }}</div>
          </div>
        </ClientOnly>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from '@nuxtjs/composition-api'
import Editor, { EditorOptions } from '@toast-ui/editor'

export default defineComponent({
  setup () {
    const editorEl = ref<HTMLElement | null>(null)
    const editor = ref<Editor | null>(null)

    if (process.client) {
      const Editor = require('@toast-ui/editor')
      watch(() => editorEl.value, (editorElValue) => {
        if (editorElValue) {
          const editorOption: EditorOptions = {
            el: editorElValue,
            height: '500px',
            initialEditType: 'wysiwyg',
            previewStyle: 'vertical'
          }
          editor.value = new Editor(editorOption)
        }
      })
    }

    const htmlResult = ref<string>('')
    const handleClick = () => {
      if (editor.value) {
        htmlResult.value = editor.value.getHtml()
      }
    }

    return {
      editorEl,
      htmlResult,
      handleClick
    }
  }
})
</script>

<style src="codemirror/lib/codemirror.css"></style>
<style src="@toast-ui/editor/dist/toastui-editor.css"></style>
<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

</style>
