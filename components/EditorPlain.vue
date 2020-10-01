<template>
  <div>
    <ClientOnly>
      <div ref="editorEl"></div>
    </ClientOnly>
    <div>
      <button @click="handleClick">
        result
      </button>
      <div>{{ htmlResult }}</div>
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
          const editorOptions: EditorOptions = {
            el: editorElValue,
            height: '300px',
            initialEditType: 'wysiwyg',
            previewStyle: 'vertical'
          }
          editor.value = new Editor(editorOptions)
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
