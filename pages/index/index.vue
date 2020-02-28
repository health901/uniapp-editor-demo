<template>
    <view class="content">
        <view class="text-area" v-if="!showEditor">
            <view>简介：</text>
                <view auto-height v-html="html" class="html"></view>
                <button @tap="openEditor">编辑</button>
            </view>
        </view>
        <meditor v-else class="editor" @cancel="hideEditor" @save="saveEditor" :html="html"
            :imageUploader="uploadImg" :muiltImage="true"></meditor>
    </view>
</template>

<script>
    import meditor from '@/components/editor/editor.vue';
    export default {
        components: {
            meditor
        },
        data() {
            return {
                showEditor:false,
                html: '<b style="color:#ff0000">Hello</b>'
            }
        },
        methods: {
            openEditor: function() {
                this.showEditor = true
            },
            hideEditor: function() {
                this.showEditor = false
            },
            saveEditor: function(e) {
                this.html = e.html
                this.hideEditor()
            },
            uploadImg: function(img, callback) {
                //上传图片逻辑,将图片链接传给回调函数
                callback(img)
            }
        }
    }
</script>

<style>
    view{
        box-sizing: border-box;
    }
    .html{
        width: 100%;
    }
    .editor{
       width: 100%;
    }
</style>
