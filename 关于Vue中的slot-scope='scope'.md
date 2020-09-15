# 关于Vue中使用ElementUI的slot-scope='scope'

```vue
<template>
	<el-table :data='tableData' style='width:100%'>
    	//---:data='用户存放请求数据回来的数组'
        <el-table-column label='索引值'>
    		<template slot-scope='scope'>
                //---这里取到当前单元格
                <span>{{scope.$index}}</span>//--- scope.$index就是索引
			</template>
    	</el-table-column>
		<el-table-column label='标题'>
			<template slot-scope='scope'>
				//--- 这里取到单元格
            	<span>{{scope.row.title}}</span>
				//--- scope.row 直接取到该单元格对象，就是数组里的元素对象，即tableData[scope.$index]
				//--- .title是对象里面的title属性值
            </template>
		</el-table-column>
    </el-table>
</template>
```

