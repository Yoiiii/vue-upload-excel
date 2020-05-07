# vue-upload-excel
> vue-upload-excel是一个基于Vue2.0和XLSX的Vue组件，用于获取和显示Excel中数据。

## 引入
```
//将目录中components中的UploadExcel.vue放入项目中并引用
import UploadExcel from "@/components/UploadExcel.vue";
//另需引用element UI buttom 和 table组件
```
##运行示例
```
npm install
npm run serve
```
## 快速上手
```
<template>
  <div class="app">
    <UploadExcel :beforeUpload="beforeUpload" :onSuccess="handleSuccess" :showData="showData" @tableData="excelData"></UploadExcel>
  </div>
</template>

<script>
import UploadExcel from "@/components/UploadExcel.vue";
export default {
  name: "app",
  components: {
    UploadExcel
  },
  data() {
    return {
      showData: true
    };
  },
  methods: {
    // 文件读取前执行
    beforeUpload(file) {
      // 取文件大小，限制文件大小超过1mb
      const isLt1M = file.size / 1024 / 1024 < 1;
      if (isLt1M) {
        return true;
      }
      this.$message({
        message: "上传的Excel文件不能大于1mb.",
        type: "warning"
      });
      return false;
    },
    // 文件读取后执行
    handleSuccess({ headerlist, resultslist, sheetList }) {
      console.log("headerlist",headerlist);
      console.log("resultslist",resultslist);
      console.log("sheetList",sheetList);
    },
    excelData(data){
      console.log("excelData",data);
    }
  }
};
</script>
```

##Props
###beforeUpload
```javascript
   beforeUpload: Function,//文件读取前执行
```
###onSuccess
```
   onSuccess: Function,//文件读取后返回返回excel数据对象，如下
    handleSuccess({ headerlist, resultslist, sheetList }) {
      console.log("headerlist",headerlist);//表头列表
      console.log("resultslist",resultslist);//表数据列表
      console.log("sheetList",sheetList);//工作表名称列表
    },
```
###showData
```
    showData: {//是否展示数据
      type: Boolean,
      default: false
    }
```

