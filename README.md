# awesomepos 快餐店收银系统

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```
## 学习心得
### 1、绘制构图，工具有MockPlus，磨刀
### 2、vue-cli搭建开发环境
``` bash
# 全局安装脚手架vue-cli
npm install vue-cli -g

# 1、创建项目有两种方式：
# 第一种：
vue init webpack awesomepos

# 第二种：
mikdir awesomepos 
cd awesomepos
vue init webpack

# 2、安装依赖
npm install

# 3、测试是否安装成功
npm run dev
```
### 3、搞定图标--Iconfont
 1 进入网站：Iconfont网址：http://www.iconfont.cn
 2 点击网站上方的“官方图标库”，选择自己喜欢的图标。在这里我选择天猫的图标库。
 3 选择好自己喜欢的图标，你可以有两个选择，下载代码 和 添加至项目。
 4 我们这两选择添加至项目，然后新建项目，并输入名称。
 5 项目添加好后，会自动给我们转入到我们项目库中。点击查看在线链接。
 6 生产css引入的代码，生成后就可以在项目首页index.html引入了。
 引用：
```
<link rel="stylesheet" href="http://at.alicdn.com/t/font_wyhhdpv5lhvbzkt9.css">
```
 使用图标，
```
<i class="icon iconfont icon-hanbao"></i>
```

### 4、引入element-ui
```
# 安装
npm i element-ui --save

# 完整引入项目
# 在main.js中写入：
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-default/index.css'
...
Vue.use(ElementUI)
```
### 解决100%高的问题 在页面中使用了Element组件，这样他会自动给我们生产虚拟DOM，我们无法设置高度100%；
```
# 利用javascript原生方法，来设置100%高度问题
mounted () {
    var orderHeight=document.body.clientHeight;
    document.getElementById("order-list").style.height = orderHeight + 'px'
}
```

### 5、Axios请求数据
```
# 安装axios
npm i axios --save

# 在哪里使用，就在哪里引入axios
import axios from 'axios'

# 用法
axios.get('地址').then(reponse => {console.log(reponse)}).catch(error => {console.log(error)})
```

### 6、核心功能
1、添加商品
```
# 重点，过滤数组的方法filter（条件）：返回满足条件的新数组
methods:{
    //添加订单列表的方法
    addOrderList(goods){
        this.totalCount=0; //汇总数量清0
        this.totalMoney=0;
        let isHave=false;
        //判断是否这个商品已经存在于订单列表
        for (let i=0; i<this.tableData.length;i++){
            console.log(this.tableData[i].goodsId);
            if(this.tableData[i].goodsId==goods.goodsId){
                isHave=true; //存在
            }
        }
        //根据isHave的值判断订单列表中是否已经有此商品
        if(isHave){
            //存在就进行数量添加
                let arr = this.tableData.filter(o => o.goodsId == goods.goodsId);
                arr[0].count++;
                //console.log(arr);
        }else{
            //不存在就推入数组
            let newGoods={goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
                this.tableData.push(newGoods);
        }
        //进行数量和价格的汇总计算
        this.tableData.forEach((element) => {
            this.totalCount+=element.count;
            this.totalMoney=this.totalMoney+(element.price*element.count);   
        });
    }
}
```

2、删除单个商品
```
//删除单个商品
delSingleGoods(goods){
    console.log(goods);
    this.tableData=this.tableData.filter(o => o.goodsId !=goods.goodsId); // 返回满足条件的新数组
},
```

3、汇总数量和金额
```
//汇总数量和金额
getAllMoney(){
    this.totalCount=0;
    this.totalMoney=0;
    if(this.tableData){
        this.tableData.forEach((element) => {
            this.totalCount+=element.count;
            this.totalMoney=this.totalMoney+(element.price*element.count);
        });
    }
}
```

4、模拟结账
```
checkout() {
    if (this.totalCount!=0) {
        this.tableData = [];
        this.totalCount = 0;
        this.totalMoney = 0;
        this.$message({
            message: '结账成功，感谢你又为店里出了一份力!',
            type: 'success'
        });
    }else{
        this.$message.error('不能空结。老板了解你急切的心情！');
    }
}
```

5、项目打包和上线
### 1、 打开config/index.js文件会看到一个build属性，这里就是打包的基本配置了，你在这里可以修改打包的目录，打包的文件名。最重要的是一定要把绝对目录改为相对目录。这样才能保证我们打包出去的项目可以正常预览。
```
assetsPublicPath:'./'
```

### 2、打包
```
npm run build
```

## 技术栈
 vue-router，Element，Axios，iconFont等
