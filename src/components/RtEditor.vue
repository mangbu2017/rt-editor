<template>
    <div class="tinymce-vue">
        <h1>my-vueTinymce</h1>
        <editor v-model="msg" :init="editorInit" />
        <div v-html="msg" class="msg"></div>
        <textarea v-model="msg" cols="30" rows="10"></textarea>
    </div>
</template>
<script>
    import ajax from 'axios';
    import tinymce from 'tinymce/tinymce';
    import Editor from '@tinymce/tinymce-vue';
    import 'tinymce/themes/modern/theme';
    import 'tinymce/plugins/image';
    import 'tinymce/plugins/link';
    import 'tinymce/plugins/code';
    import 'tinymce/plugins/table';
    import 'tinymce/plugins/lists';
    import 'tinymce/plugins/contextmenu';
    import 'tinymce/plugins/wordcount';
    import 'tinymce/plugins/colorpicker';
    import 'tinymce/plugins/textcolor';
    import 'tinymce/plugins/imagetools';

    export default {
        name: 'HelloWorld',
        data() {
            return {
                msg: '<b>Welcome</b> to Your Vue.js App',
                editorInit: {
                    language_url: '/static/tinymce/langs/zh_CN.js',
                    language: 'zh_CN',
                    // 皮肤
                    skin_url: '/static/tinymce/skins/lightgray',
                    // 功能插件
                    plugins: 'image link code table lists contextmenu wordcount colorpicker textcolor imagetools',
                    height: 300, 
                    image_advtab: true,
                    images_upload_handler: this.images_upload_handler,
                },
            };
        },
        methods: {
            images_upload_handler(blobInfo, success, failure) {
                const formData = new FormData();
                console.log(formData, blobInfo.blob, blobInfo.filename);
                formData.append('upfile', blobInfo.blob(), blobInfo.filename());
                ajax({
                    methods: 'post',
                    url: '',
                    data: formData,
                }).then(res => {
                    success(res.data.url);
                }).catch(err => {
                    failure('上传失败');
                });
                
            },
        },
        mounted() {
            tinymce.init({})
        },
        components: {
            Editor,
        }
    }
</script>
<style scoped>
    .msg {
        width: 200px;
        height: 200px;
        margin: 0 auto;
        background-color: #000;
        color: #fff;
    }
</style>
