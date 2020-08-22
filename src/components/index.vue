<template>
    <div class="in-coder-panel">
        <textarea ref="textarea"></textarea>
    </div>
</template>
<script>
import 'codemirror/mode/shell/shell.js'
import CodeMirror from 'codemirror'
// 核心样式
import 'codemirror/lib/codemirror.css'
// 引入主题后还需要在 options 中指定主题才会生效
import 'codemirror/theme/night.css'
import 'codemirror/addon/hint/anyword-hint.js';
import 'codemirror/addon/hint/show-hint.css';
import 'codemirror/addon/hint/show-hint.js';
export default {
    name: "Index",
    data() {
        return {
            mode: 'shell',
            options: {
                tabSize: 4,
                theme: 'night',
                lineNumbers: true,
                line: true,
                extraKeys: { 'Ctrl': 'autocomplete', 'Enter': this.enter}
            },
            code: 'aaa\nddd\n'
        }
    },
    mounted() {
        // 初始化编辑器实例，传入需要被实例化的文本域对象和默认配置
        this.coder = CodeMirror.fromTextArea(this.$refs.textarea, this.options)
        this._initialize()
    },
    methods :{
        // 初始化
        _initialize() {
            // 编辑器赋值
            this.coder.setValue(this.code)
            this.coder.setSize('100%', '600px')
            // 支持双向绑定
            this.coder.on('change', (coder) => {
                this.code = coder.getValue()
                if (this.$emit) {
                    this.$emit('input', this.code)
                }
            })

            // 尝试从父容器获取语法类型
            if (this.language) {
                // 获取具体的语法类型对象
                const modeObj = this._getLanguage(this.language)

                // 判断父容器传入的语法是否被支持
                if (modeObj) {
                    this.mode = modeObj.label
                }
            }
        },
        enter() {
            let str = '\nhaha'
            this.code = this.code.concat(str)
            console.log(this.code)
        }
    }
}
</script>
<style scoped>
</style>