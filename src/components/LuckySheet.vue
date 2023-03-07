<template>
  <div style="position: absolute; top: 0">
    <input id="uploadBtn" type="file" @change="loadExcel" />

    <span>Or Load remote xlsx file:</span>

    <select v-model="selected" @change="selectExcel">
      <option disabled value="">Choose</option>
      <option v-for="option in options" :key="option.text" :value="option.value">
        {{ option.text }}
      </option>
    </select>

    <a href="javascript:void(0)" @click="downloadExcel">Download source xlsx file</a>
  </div>
  <div id="stevenysheet"></div>
  <div v-show="isMaskShow" id="tip">Downloading</div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { exportExcel } from '../utils/export'
import { isFunction } from '../utils/is'
import StevenyExcel from 'stevenyexcel'

const isMaskShow = ref(false)
const selected = ref('')
const jsonData = ref({})
const options = ref([
  { text: 'Money Manager.xlsx', value: 'https://minio.cnbabylon.com/public/stevenysheet/money-manager-2.xlsx' },
  {
    text: 'Activity costs tracker.xlsx',
    value: 'https://minio.cnbabylon.com/public/stevenysheet/Activity%20costs%20tracker.xlsx',
  },
  {
    text: 'House cleaning checklist.xlsx',
    value: 'https://minio.cnbabylon.com/public/stevenysheet/House%20cleaning%20checklist.xlsx',
  },
  {
    text: 'Student assignment planner.xlsx',
    value: 'https://minio.cnbabylon.com/public/stevenysheet/Student%20assignment%20planner.xlsx',
  },
  {
    text: 'Credit card tracker.xlsx',
    value: 'https://minio.cnbabylon.com/public/stevenysheet/Credit%20card%20tracker.xlsx',
  },
  { text: 'Blue timesheet.xlsx', value: 'https://minio.cnbabylon.com/public/stevenysheet/Blue%20timesheet.xlsx' },
  {
    text: 'Student calendar (Mon).xlsx',
    value: 'https://minio.cnbabylon.com/public/stevenysheet/Student%20calendar%20%28Mon%29.xlsx',
  },
  {
    text: 'Blue mileage and expense report.xlsx',
    value: 'https://minio.cnbabylon.com/public/stevenysheet/Blue%20mileage%20and%20expense%20report.xlsx',
  },
])

const loadExcel = (evt) => {
  const files = evt.target.files
  if (files == null || files.length == 0) {
    alert('No files wait for import')
    return
  }

  let name = files[0].name
  let suffixArr = name.split('.'),
    suffix = suffixArr[suffixArr.length - 1]
  if (suffix != 'xlsx') {
    alert('Currently only supports the import of xlsx files')
    return
  }
  StevenyExcel.transformExcelToSteveny(files[0], function (exportJson, stevenysheetfile) {
    if (exportJson.sheets == null || exportJson.sheets.length == 0) {
      alert('Failed to read the content of the excel file, currently does not support xls files!')
      return
    }
    console.log('exportJson', exportJson)
    jsonData.value = exportJson

    isFunction(window?.stevenysheet?.destroy) && window.stevenysheet.destroy()

    window.stevenysheet.create({
      container: 'stevenysheet', //stevenysheet is the container id
      showinfobar: false,
      data: exportJson.sheets,
      title: exportJson.info.name,
      userInfo: exportJson.info.name.creator,
    })
  })
}
const selectExcel = (evt) => {
  const value = selected.value
  const name = evt.target.options[evt.target.selectedIndex].innerText

  if (value == '') {
    return
  }
  isMaskShow.value = true

  StevenyExcel.transformExcelToStevenyByUrl(value, name, (exportJson, stevenysheetfile) => {
    if (exportJson.sheets == null || exportJson.sheets.length == 0) {
      alert('Failed to read the content of the excel file, currently does not support xls files!')
      return
    }
    console.log('exportJson', exportJson)
    jsonData.value = exportJson

    isMaskShow.value = false

    isFunction(window?.stevenysheet?.destroy) && window.stevenysheet.destroy()

    window.stevenysheet.create({
      container: 'stevenysheet', //stevenysheet is the container id
      showinfobar: false,
      data: exportJson.sheets,
      title: exportJson.info.name,
      userInfo: exportJson.info.name.creator,
    })
  })
}
const downloadExcel = () => {
  // const value = selected.value;;
  //
  // if(value.length==0){
  //     alert("Please select a demo file");
  //     return;
  // }
  //
  // var elemIF = document.getElementById("Steveny-download-frame");
  // if(elemIF==null){
  //     elemIF = document.createElement("iframe");
  //     elemIF.style.display = "none";
  //     elemIF.id = "Steveny-download-frame";
  //     document.body.appendChild(elemIF);
  // }
  // elemIF.src = value;
  exportExcel(stevenysheet.getAllSheets(), '下载')
}

// !!! create stevenysheet after mounted
onMounted(() => {
  stevenysheet.create({
    container: 'stevenysheet',
  })
})
</script>

<style scoped>
#stevenysheet {
  margin: 0px;
  padding: 0px;
  position: absolute;
  width: 100%;
  left: 0px;
  top: 30px;
  bottom: 0px;
}

#uploadBtn {
  font-size: 16px;
}

#tip {
  position: absolute;
  z-index: 1000000;
  left: 0px;
  top: 0px;
  bottom: 0px;
  right: 0px;
  background: rgba(255, 255, 255, 0.8);
  text-align: center;
  font-size: 40px;
  align-items: center;
  justify-content: center;
  display: flex;
}
</style>
