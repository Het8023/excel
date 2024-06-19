<template>
    <el-upload
        class="avatar-uploader-excel"
        ref="uploadRef"
        :limit="limitFile"
        accept=".xlsx, .xls"
        action="#"
        :file-list="fileList"
        :on-change="onChangeFun"
        :auto-upload="false"
        drag
        :on-exceed="handleExceed"
        multiple>
        <i class="el-icon-upload"></i>
        <div class="el-upload__text">
            将文件拖拽到此处，或
            <em>点击上传</em>
        </div>
        <div class="el-upload__tip text-center">jpg/png files with a size less than 500kb</div>
    </el-upload>
    <el-button type="primary" @click="submitFileForm">确定</el-button>
    <el-button @click="handleCloseUpload">取消</el-button>
</template>

<script setup>
import { ref } from "vue";
let fileList = ref([]);
let limitFile = ref(3);
const onChangeFun = (file, list) => {
    // 判断上传文件是否已存在
    //     let existFile = list.slice(0, list.length - 1).find((f) => f.name === file.name);
    //     if (existFile) {
    //         useMessage().error("当前文件已经存在!");
    //         list.pop();
    //     }
    //     fileList = list;
    console.log(file);
    console.log(list);
};
const submitFileForm = () => {
    if (!fileList.length) {
        useMessage().error("请上传至少一个文件!");
        return;
    }
    let formData = new FormData();
    fileList.forEach((item) => {
        formData.append("file", item.raw);
    });
    formData.append("id", "");
    console.log(fileList.value);
    // 这里写接口逻辑，将formData传给后端
};
const handleExceed = () => {
    useMessage().error(`最多上传${limitFile}个文件，请删除后重新上传！`);
};
</script>
