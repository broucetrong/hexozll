---
title: EasyUI - 对 Datagrid 数据表格的操作
categories:
- 前端
tags:
- EasyUI
---
#### EasyUI 中对datagrid进行操作的常用语句：
<!-- more -->
```
//根据rowData获得rowIndex
var rowIndex = $("#demo_datagrid").datagrid("getRowIndex", rowData);
---------------------------------------------------------------
//根据rowIndex获得rowData
$('#datagrid_id').datagrid('unselectAll');
$('#datagrid_id').datagrid('selectRow', rowIndex);
var rowData = $('#datagrid_id').datagrid('getSelected');
$('#datagrid_id').datagrid('unselectRow', rowIndex);
---------------------------------------------------------------
// 刷新索引行，在行数据修改后
$('#demo_datagrid').datagrid('refreshRow', rowIndex);
---------------------------------------------------------------
//新增行
$('#datagrid_id').datagrid('appendRow', {});
//获取新增行
rowIndex = $('#datagrid_id').datagrid('getRows').length - 1;
---------------------------------------------------------------
//编辑索引行
$('#datagrid_id').datagrid('selectRow', rowIndex)
    .datagrid('beginEdit', rowIndex);
//退出编辑索引行
$('#datagrid_id').datagrid('endEdit', rowIndex);
//删除索引行
$('#datagrid_id').datagrid('cancelEdit', rowIndex)
    .datagrid('deleteRow', rowIndex);
//保存修改
$('#datagrid_id').datagrid('acceptChanges');
---------------------------------------------------------------
//校验正在编辑的索引行
var result = $('#datagrid_id').datagrid('validateRow', rowIndex);
//执行form的校验
var result = $('#column_form').form('validate');
---------------------------------------------------------------
//获得索引行的编辑器
var editor = $('#datagrid_id').datagrid('getEditor', {
    index: rowIndex,
    field: 'tableName'
});
//设定“表名”不可修改
$(editor.target).combobox({
    readonly: true
});

```