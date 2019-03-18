<template>
  <div>
    <el-table
      :data="tableData"
      size="mini"
      border
      :highlight-current-row="tableAttribute.highlight_current_row"
      :stripe="tableAttribute.stripe"
      @cell-click="cellClick"
      style="width: 100%"
      :row-class-name="tableRowClassName">
      <el-table-column
        v-for="item in tableTitle"
        :key="item.prop"
        :prop="item.prop"
        :label="item.label"
        :width="item.width">
        <template slot-scope="{row, column, $index}">
          <input style="width: 100%" v-if="item.isEdit"  v-model="row.value[item.index]" v-on:blur="cellBlur($index,item.index)">
          <span v-if="!item.isEdit">{{row.value[item.index]}}</span>
        </template>
      </el-table-column>
    </el-table>
    <el-button type="primary" v-on:click="print">主要按钮</el-button>
  </div>
</template>

<script>
export default {
  name: 'table',
  mounted: function () {
    this.dataFormat()
  },
  data () {
    return {
      tableTitle: [
        {
          prop: 'date',
          label: '日期',
          width: 180,
          isEdit: false,
          index: 0
        },
        {
          prop: 'name',
          label: '名称',
          width: 100,
          isEdit: false,
          index: 1
        },
        {
          prop: 'qty',
          label: 'qty',
          width: 100,
          isEdit: true,
          index: 2
        }
      ],
      tableData: [],
      sourceData: [
        {
          date: '2016-05-02',
          name: '张三',
          qty: 1
        },
        {
          date: '2016-05-02',
          name: '张三2',
          qty: 12
        },
        {
          date: '2016-05-02',
          name: '张三3',
          qty: 13
        },
        {
          date: '2016-05-02',
          name: '张三3',
          qty: 13
        },
        {
          date: '2016-05-02',
          name: '张三3',
          qty: 13
        },
        {
          date: '2016-05-02',
          name: '张三3',
          qty: 13
        },
        {
          date: '2016-05-02',
          name: '张三3',
          qty: 13
        }
      ],
      tableAttribute: {
        stripe: true,
        highlight_current_row: true
      }
    }
  },
  methods: {
    print: function () {
      console.log(this.tableData)
    },
    cellBlur: function (indexY, indexX) {
      console.info(indexY + '======' + indexX)
      console.info(indexY + '======' + this.tableData[indexY].value[indexX])
    },
    dataFormat: function () {
      var list = this.sourceData
      var title = this.tableTitle
      for (var i = 0; i < list.length; i++) { // 所有的行
        var temp = list[i]
        var tempArray = []
        for (var j = 0; j < title.length; j++) { // 遍历一行数据进行转换
          tempArray.push(temp[title[j].prop])
        }
        var tempMap = {}
        tempMap.value = tempArray
        this.tableData.push(tempMap)
      }
    },
    tableRowClassName ({row, rowIndex}) {
      if (rowIndex % 2 === 0) {
        return 'warning-row'
      }
      return ''
    },
    cellClick (row, column, cell, event) {
      console.info(row + '=====' + JSON.stringify(cell))
    }
  }

}
</script>

<style>
  .el-table .warning-row {
    background: #e0e0e0;
  }
</style>
