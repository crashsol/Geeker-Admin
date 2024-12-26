<template>
  <!-- <ListTable :options="option" ref="listTable"></ListTable> -->
  <div id="etable" style="width: 800px; height: 600px"></div>
</template>
<script lang="ts" setup>
import { onMounted, onUnmounted, ref, watch } from "vue";
import { VTable } from "@visactor/vue-vtable";
import { InputEditor, DateInputEditor, ListEditor, TextAreaEditor } from "@visactor/vtable-editors";
const input_editor = new InputEditor();
const date_editor = new DateInputEditor();
const list_editor = new ListEditor({
  values: ["启用", "停止"]
});
const textarea_editor = new TextAreaEditor();

VTable.register.editor("input-editor", input_editor);
VTable.register.editor("date-editor", date_editor);
VTable.register.editor("opt_editor", list_editor);
VTable.register.editor("textarea-editor", textarea_editor);

// const listTable = ref();
const option: VTable.ListTableConstructorOptions = {
  editCellTrigger: "click",
  widthMode: "standard",
  columns: [
    {
      field: "name",
      title: "name",
      sort: true,
      width: "auto",
      editor: "input-editor"
    },
    {
      field: "age",
      title: "age",
      editor: "input-editor"
    },
    {
      field: "sex",
      title: "sex",
      editor: "input-editor"
    },
    {
      field: "phone",
      title: "phone",
      editor: "input-editor"
    },
    {
      field: "date",
      title: "data",
      editor: "date-editor"
    },
    {
      field: "address",
      title: "address",
      editor: "opt_editor"
    }
  ],
  records: [
    { name: "zhang_san", age: 20, sex: "female", date: "2024-12-26", phone: "123456789", address: "启用" },
    { name: "li_si", age: 30, sex: "female", date: "2024-12-26", phone: "23456789", address: "启用" },
    { name: "wang_wu", age: 40, sex: "male", date: "2024-12-26", phone: "3456789", address: "启用" }
  ]
};
watch(option, (old, ddd) => {
  console.log(old, ddd);
});
let tableInstance;
onMounted(() => {
  tableInstance = new VTable.ListTable(document.getElementById("etable")!, option);
  tableInstance.on("change_cell_value", arg => {
    console.log(arg);
  });
});
onUnmounted(() => {
  tableInstance = null;
});
</script>
