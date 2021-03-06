# D3_ES6
D3.js+Es6+webpack构建人物关系图(力导向图)
功能列表：
1. 增加下载SVG转PNG功能，图片尺寸超出可视区域也能够下载全部显示出来
2. 增加图谱放大缩小平移功能
3. 增加图谱初始化加载时自动缩放功能
4. 增加导出excel功能,配合后台工具类达到导入excel的功能
5. 增加右键菜单功能(删除,编辑)
6. 增加拖拽添加连线功能
7. 增加鼠标点击画布增加节点功能,支持批量添加并取消连续点击连续添加的功能
8. 增加右键删除节点和左侧工具栏删除节点功能
9. 增加环形布局
10. 增加矩形布局

在此大神的代码基础上,进行了修改,源代码地址::https://github.com/zhangzn3/D3-Es6   

使用文档:
1.index.htm作为程序入口页面
![Image](https://github.com/f2733938/img-folder/blob/master/1226716-20190712090417411-1558682042.png)
![Image](https://github.com/f2733938/img-folder/blob/master/1226716-20190712090431757-1906131820.png)
2.简单解析核心js  home.bundle.js      D3-Es6-master\docs\js
(1) 初始加载数据 _api2.default.getData().always(function (rps)方法
![Image](https://github.com/f2733938/img-folder/blob/master/1226716-20190712090446716-1800951716.png)
(2) 添加节点  d3.select('#J_AddNode').on("click.add-node", function ()方法
![Image](https://github.com/f2733938/img-folder/blob/master/1226716-20190712090457429-1823432860.png)
(3) 添加连线,建立对应关系,双向线代码部分理应删除
![Image](https://github.com/f2733938/img-folder/blob/master/1226716-20190712090505362-751164846.png)
(4) 导出excel  exportExcel: function exportExcel(json)
![Image](https://github.com/f2733938/img-folder/blob/master/1226716-20190712090512207-2051806503.png)
(5) 显示数据
![Image](https://github.com/f2733938/img-folder/blob/master/1226716-20190712090522096-1206398169.png)
3.使用方式
(1)  添加节点
     点击添加节点,弹出输入框,输入信息后点击添加即为添加成功
(2)  批量添加节点(新增)
  添加多个有内容节点时,节点名称用|分隔,可以复用节点标题和节点注释,节点数量不必填写
  只填写节点数量时,生成对应个数的空白节点
(3)  删除节点
     选中该节点,点击删除节点,如果该节点有子级时,子级节点并不会消失,变成游离状态
(4)  添加连线
     点击添加连线,点击父级节点,鼠标左键进行拖动至子级节点,箭头由父级指向子级
(5)  删除连线
     同删除节点

3.存在的问题(说明)
(1) 新增数据时,需要修改 data.js 文件 docs\docs\datajs\data.js
编辑时的数据来源mockData 见6
(2) 原始根节点(顶级节点),在excel 没有数据,需要手动添加一行.(已修复)
在添加数据时处理,再次添加次级根节点不需要操作excel

顶级节点的默认Id 为root,同(3)图,导出Excel时,与顶级节点关联的,显示如下
(3) 进行删除节点操作时,只能选择一个节点,多选或不选时,提示内容,当删除异常时,使用鼠标右键删除
(4) 目前导出的excel名称默认为excel+毫秒,工作表名称默认名称为mySheet
(5) 删除节点或删除连线时,可以在该节点进行鼠标右键操作
  测试数据   cscoIV期评估
4.  导入数据  后台修改第二版  (本项目不提供原码,若逻辑简单,可直接修改数据)
 对原有的excel 进行导入编辑时,需要在后台生成对应的json 文件,excel 文件不可有跳转数据并且必须要有顶级节点
 (1) .  使用TestReadPoi 生成json 文件=
       配置读取文件路径,修改在该类下的filePath
   执行junit  ,得到json  文件
 (2) .  将数据复制进data.js 中
  data.js 文件位置 \docs\docs\datajs\data.js


目前生成的 json 数据和d3  所需要的数据一致     

实现导入excel功能时,第一版完全是前端进行解析,但是得到json 后,无法再次调用绘制D3 的方法(前端水平限制了我),只能按照从后台生成json ,然后整体复制的方法,方法low了一些,但是整体功能都能实现
5. 与原版差异列表
(1). 新增节点取消随机数生成,采用表格输入
(2). 增加批量添加节点的功能
(3). 导出excel 时,新增导出字段,不仅仅是source target,见1(4)
(4). 在原有导出excel功能,添加配合后台工具类达到导入excel的功能
(5). 增加右键菜单功能(删除,编辑)
(6). 修改节点显示
(7). 增加节点时取消连续点击连续添加的功能
