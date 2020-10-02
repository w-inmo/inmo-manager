<template>
    <el-dialog
        :visible.sync="visible"
        :title="article.title"
        width="60%">
        <modify-form class="modify-form" :form="article"></modify-form>
        <span slot="footer" class="dialog-footer">
            <el-button @click="$emit('close')">取 消</el-button>
            <el-button type="primary" @click="onCommit">修改</el-button>
        </span>
    </el-dialog>
</template>

<script>

    import ModifyForm from '../ModifyForm'

    export default {
        name: 'Mofidy',
        props: {
            modifyData: {
                type: [Object, null],
                default: null
            }
        },
        components: {
            ModifyForm
        },
        watch: {
            modifyData(val) {
                if (val) val.tags = val.tags.split(',')  
            }
        },
        computed: {
            visible: {
                get() {
                    return this.modifyData !== null
                },
                set() {
                    this.$emit('close')
                }
            },
            article() {
                return this.visible ? this.modifyData : {
                    title: '',
                    content: '',
                    tags: '',
                    category: '',
                    pubdate: ''
                }
            }
        },
        methods: {
            onCommit() {
                this.$emit('commit', this.modifyData)
            }
        }
    }

</script>

<style lang="stylus" scoped>

    .modify-form
        height 50vh

</style>
