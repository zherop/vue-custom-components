<template>
    <div class="json-view-container">
        <codemirror ref="codeMirror"
        :options="options"
        @input="handleChange"
        @inputRead="handlePaste"
        :value="code" style="border: 1px solid #ddd;">
        </codemirror>
    </div>
</template>

<script>
import { codemirror } from 'vue-codemirror'
import 'codemirror/lib/codemirror.css'
import 'codemirror/mode/javascript/javascript.js'
import 'codemirror/addon/edit/matchbrackets.js'
import 'codemirror/addon/comment/continuecomment.js'
import 'codemirror/addon/comment/comment.js'
import 'codemirror/addon/selection/active-line.js'
import 'codemirror/theme/xq-light.css'

export default {
  props: {
    value: {
      type: [String, Object],
      required: true
    }
  },
  components: {
    codemirror
  },
  data() {
    return {
      code: '',
      isObject: false,
      options: {
        theme: 'xq-light',
        lineNumbers: true,
        line: true,
        matchBrackets: true,
        autoCloseBrackets: true,
        styleActiveLine: true,
        mode: 'application/ld+json',
        lineWrapping: true
      }
    }
  },

  watch: {
    code() {
      debugger
      let returnValue = this.code
      if (this.isObject) {
          returnValue = JSON.parse(this.code)
      }
      this.$emit('input',returnValue)
    }
  },

  created() {
    if (this.value instanceof Object) {
      this.isObject = true
    }
    let json = ''
    if (this.isObject) {
      json = JSON.stringify(this.value, null, '  ')
    } else {
      let codeJson = JSON.parse(this.value)
      json = JSON.stringify(codeJson, null, '  ')
    }
    this.code = json
  },

  methods: {
    handleChange(newCode) {
      this.code = newCode
    },

    handlePaste(instance, val) {
      if (val.origin === 'paste') {
        let codeJson = JSON.parse(this.code)
        this.code = JSON.stringify(codeJson, null, '  ')
      }
    }
  }
}
</script>

<style scoped>
.json-view-container {
  display: inline-block;
  width: 100%;
}
</style>