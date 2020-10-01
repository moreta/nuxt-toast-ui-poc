<template>
  <div>
    <ClientOnly>
      <editor
        ref="editor"
        height="300px"
        initialEditType="wysiwyg"
        previewStyle="vertical"
        :options="editorOptions"
      ></editor>
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
import { defineComponent, ref } from '@nuxtjs/composition-api'
import { Editor } from '@toast-ui/vue-editor'

export default defineComponent({
  setup () {
    const editor = ref<Editor | null>(null)

    const editorOptions = ref<object>({})

    const htmlResult = ref<string>('')
    const handleClick = () => {
      if (editor.value) {
        htmlResult.value = editor.value.invoke('getHtml')
      }
    }

    return {
      editor,
      editorOptions,
      htmlResult,
      handleClick
    }
  }
})
</script>
