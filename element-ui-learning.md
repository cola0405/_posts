---
title: element-ui-learning
date: 2023-02-27 16:39:00
tags:
categories:
---





## 弹性布局







## layout

**占满全屏幕**

```css
<style>
    html,body,#app{
        height:100%;
        margin: 0px;
        padding: 0px;
    }
    .el-container{
      height: 100%;
    }
</style>

```





### 侧边栏颜色



不是el-menu、 el-aside 的background







## aside

### icon

```html
<el-menu-item>
	<i class="el-icon-message"></i> 1
</el-menu-item>
```







## css绑定



### id

```css
#difficulty {
  text-align: left;
}
```

找到 id 为 difficulty 的





### tag

```css
.el-menu{
  height: 100%;
}
```

指定标签





## table

### column 靠右

```html
			<el-table-column
                id="difficulty"
                align="right"
                prop="difficulty"
                label="Difficulty">
            </el-table-column>
```





## selector

```html
<el-select id="difficulty-select" v-model="value" placeholder="Select" v-		on:change="select_difficulty(value)">
    <el-option
               v-for="item in options"
               :key="item.value"
               :label="item.label"
               :value="item.value">
    </el-option>
</el-select>
```



```js
methods :{
    select_difficulty : function (v){
      alert(v);
    }
}
```









## filter-method

```
this method will be called multiple times for each row
a row will display if one of the calls returns true
```



![image-20230228164410194](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20230228164410194.png)



```html
          <el-table
              :data="tableData"
              style="width: 100%">
            <el-table-column
                prop="id"
                label="id"
                width="180">
            </el-table-column>
            <el-table-column
                align="center"
                prop="name"
                label="题目">
            </el-table-column>
            <el-table-column
                id="difficulty"
                :filters="[{ text:'简单', value: '简单'}, { text:'中等', value: '中等'}, { text:'困难', value: '困难'}]"
                :filter-method="filter_difficulty"
                align="right"
                prop="difficulty"
                label="难度">
            </el-table-column>
          </el-table>
```



```js
export default {
  name: 'App',
  data: function (){
    return {
      names: ["Cola", "Amy", "Coco"],
      content : "Cola",
      tableData: [{
        id: '1',
        name: '硬币',
        difficulty: '简单'
      }, {
        id: '2',
        name: '开关灯',
        difficulty: '中等'
      }, {
        id: '3',
        name: '装箱',
        difficulty: '困难'
      }, {
        id: '4',
        name: '吃冰棍',
        difficulty: '困难'
      }],
      options: [{
        value: '简单',
        label: '简单'
      }, {
        value: '中等',
        label: '中等'
      }, {
        value: '困难',
        label: '困难'
      }],
      value: '简单'
    }
  },
  methods :{
    filter_difficulty : function (value, row){
      return row.difficulty === value;
    }
  }
}
```







