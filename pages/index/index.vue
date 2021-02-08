<template>
    <view class="content">
        <view class="text-area" v-if="!showEditor">
            <view>
                <text>简介：</text>
                <view auto-height v-html="html" class="html"></view>
                <button @tap="openEditor">编辑</button>
                <button @tap="changeHtml(1)" style="margin-top: 10rpx;">设置HTML-1</button>
                <button @tap="changeHtml(2)" style="margin-top: 10rpx;">设置HTML-2</button>
            </view>
        </view>
        <robin-editor v-else class="editor" @cancel="hideEditor" @save="saveEditor" v-model="html"
            :imageUploader="uploadImg" :muiltImage="true"></robin-editor>
    </view>
</template>

<script>
    export default {
        data() {
            return {
                showEditor:false,
                html: '<b style="color:#ff0000">HTML 片段1</b>',
                html2:'<b style="color:#ff0000">HTML 片段2</b>'
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
                // v-model已实现赋值
                // this.html = e.html
                this.hideEditor()
            },
            uploadImg: function(img, callback) {
                //上传图片逻辑,将图片链接传给回调函数
                callback(img)
            },
            changeHtml(i){
                //从远程获取数据赋值
                this.html = i == 1 ? this.html : this.html2
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
        word-break: break-all;
    }
    .editor{
       width: 100%;
    }
</style>
