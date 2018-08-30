<template>
  <div class='pos'>
    <el-row>
      <el-col :span='7' class='pos-order' id='order-list'>
        <el-tabs style='padding:5px'>
          <el-tab-pane label='点餐'>
            <el-table :data='tableData' border style='width:100%;'>
              <el-table-column prop='goodsName' label='商品名称'></el-table-column>
              <el-table-column prop='count' label='数量' width='50'></el-table-column>
              <el-table-column prop='price' label='金额' width='70'></el-table-column>
              <el-table-column label='操作' width='100' fixed='right'>
                <template slot-scope='scope'>
                  <el-button type='text' size='small' @click="delSingleGoods(scope.row)">删除</el-button>
                  <el-button type='text' size='small' @click="addOrderList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="totalDiv">
              <small>数量：</small>{{totalCount}} &nbsp;&nbsp;&nbsp;&nbsp; <small>金额：</small>{{totalMoney}}
            </div>
            <div class='div-btn'>
              <el-button type='warning'>挂单</el-button>
              <el-button type='danger' @click="delAllGoods">删除</el-button>
              <el-button type='success' @click="checkout">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label='挂单'>挂单</el-tab-pane>
          <el-tab-pane label='外卖'>外卖</el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col :span='17'>
        <div class='often-goods'>
          <div class='title'>常用商品</div>
          <div class='often-goods-list'>
            <ul>
              <li v-for='(goods, index) in oftenGoods' :key='index' @click="addOrderList(goods)" style="cursor: pointer">
                <span>{{goods.goodsName}}</span>
                <span class='price'>￥{{goods.price}}</span>
              </li>
            </ul>
          </div>
        </div>
        <div class='goods-type'>
          <el-tabs>
            <el-tab-pane label='汉堡'>
              <div>
                <ul class='cookList'>
                  <li v-for='(goods, index) in type0Goods' :key='index' @click="addOrderList(goods)" style="cursor: pointer">
                    <span class='foodImg'><img :src='goods.goodsImg' width='100%'></span>
                    <span class='foodName'>{{goods.goodsName}}</span>
                    <span class='foodPrice'>￥{{goods.price}}</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label='小食'>
              <div>
                <ul class='cookList'>
                  <li v-for='(goods, index) in type0Goods' :key='index' @click="addOrderList(goods)" style="cursor: pointer">
                    <span class='foodImg'><img :src='goods.goodsImg' width='100%'></span>
                    <span class='foodName'>{{goods.goodsName}}</span>
                    <span class='foodPrice'>￥{{goods.price}}</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label='饮料'>
              <div>
                <ul class='cookList'>
                  <li v-for='(goods, index) in type0Goods' :key='index' @click="addOrderList(goods)" style="cursor: pointer">
                    <span class='foodImg'><img :src='goods.goodsImg' width='100%'></span>
                    <span class='foodName'>{{goods.goodsName}}</span>
                    <span class='foodPrice'>￥{{goods.price}}</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
            <el-tab-pane label='套餐'>
              <div>
                <ul class='cookList'>
                  <li v-for='(goods, index) in type0Goods' :key='index' @click="addOrderList(goods)" style="cursor: pointer">
                    <span class='foodImg'><img :src='goods.goodsImg' width='100%'></span>
                    <span class='foodName'>{{goods.goodsName}}</span>
                    <span class='foodPrice'>￥{{goods.price}}</span>
                  </li>
                </ul>
              </div>
            </el-tab-pane>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'Pos',
  data () {
    return {
      tableData: [],
      totalCount: 0,
      totalMoney: 0,
      oftenGoods: [
        {
          goodsId: 1,
          goodsName: '香辣鸡腿堡',
          price: 18
        },
        {
          goodsId: 2,
          goodsName: '田园鸡腿堡',
          price: 15
        },
        {
          goodsId: 3,
          goodsName: '和风汉堡',
          price: 15
        },
        {
          goodsId: 4,
          goodsName: '快乐全家桶',
          price: 80
        },
        {
          goodsId: 5,
          goodsName: '脆皮炸鸡腿',
          price: 10
        },
        {
          goodsId: 6,
          goodsName: '魔法鸡块',
          price: 20
        },
        {
          goodsId: 7,
          goodsName: '可乐大杯',
          price: 10
        },
        {
          goodsId: 8,
          goodsName: '雪顶咖啡',
          price: 18
        },
        {
          goodsId: 9,
          goodsName: '大块鸡米花',
          price: 15
        },
        {
          goodsId: 20,
          goodsName: '香脆鸡柳',
          price: 17
        }
      ],
      type0Goods: [
        {
          goodsId: 1,
          goodsImg: 'http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg',
          goodsName: '香辣鸡腿堡',
          price: 18
        }, {
          goodsId: 2,
          goodsImg: 'http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg',
          goodsName: '田园鸡腿堡',
          price: 15
        }, {
          goodsId: 3,
          goodsImg: 'http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg',
          goodsName: '和风汉堡',
          price: 15
        }, {
          goodsId: 4,
          goodsImg: 'http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg',
          goodsName: '快乐全家桶',
          price: 80
        }, {
          goodsId: 5,
          goodsImg: 'http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg',
          goodsName: '脆皮炸鸡腿',
          price: 10
        }, {
          goodsId: 6,
          goodsImg: 'http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg',
          goodsName: '魔法鸡块',
          price: 20
        }, {
          goodsId: 7,
          goodsImg: 'http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg',
          goodsName: '可乐大杯',
          price: 10
        }, {
          goodsId: 8,
          goodsImg: 'http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg',
          goodsName: '雪顶咖啡',
          price: 18
        }, {
          goodsId: 9,
          goodsImg: 'http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg',
          goodsName: '大块鸡米花',
          price: 15
        }, {
          goodsId: 20,
          goodsImg: 'http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg',
          goodsName: '香脆鸡柳',
          price: 17
        }
      ]
    }
  },
  mounted () {
    var orderHeight = document.body.clientHeight
    document.getElementById('order-list').style.height = orderHeight + 'px'
  },
  methods: {
    addOrderList (goods) {
      // 判断是有已存在该商品
      let isHave = false
      for (let i = 0; i < this.tableData.length; i++) {
        if (this.tableData[i].goodsId === goods.goodsId) {
          isHave = true
        }
      }
      // 根据判断结果编写业务逻辑，有，加数量；无，加入该商品
      if (isHave) {
        let arr = this.tableData.filter(arr => arr.goodsId === goods.goodsId)
        arr[0].count++
      } else {
        let newGoods = {
          goodsId: goods.goodsId,
          goodsName: goods.goodsName,
          price: goods.price,
          count: 1
        }
        this.tableData.push(newGoods)
      }
      this.getAllMoney()
    },
    delSingleGoods (goods) {
      this.tableData = this.tableData.filter(arr => arr.goodsId !== goods.goodsId)
      this.getAllMoney()
    },
    delAllGoods () {
      this.tableData = []
      this.totalCount = 0
      this.totalMoney = 0
    },
    getAllMoney () {
      this.totalCount = 0
      this.totalMoney = 0
      if (this.tableData) {
        this.tableData.forEach(element => {
          this.totalCount += element.count
          this.totalMoney = this.totalMoney + (element.price * element.count)
        })
      }
    },
    checkout () {
      if (this.totalCount !== 0) {
        this.tableData = []
        this.totalCount = 0
        this.totalMoney = 0
        this.$message({
          message: '结账成功!',
          type: 'success'
        })
      } else {
        this.$message.error('不能空结!')
      }
    }
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
.pos-order {
  background: #f9fafc;
  border-right: 1px solid #c0ccda;
}
.div-btn {
  margin-top: 10px;
}
.title {
  height: 20px;
  border-bottom: 1px solid #d3dce6;
  background: #f9fafc;
  padding: 10px;
  text-align: left;
}
.often-goods-list ul li {
  list-style: none;
  float: left;
  width: 12%;
  border: 1px solid #e5e9f2;
  padding: 10px;
  margin: 10px;
  background: #fff;
}
.price {
  color: #58b7ff;
}
.goods-type {
  clear: both;
  padding: 10px;
}
.cookList li{
  list-style: none;
  width:23%;
  border:1px solid #E5E9F2;
  height: auto;
  overflow: hidden;
  background-color:#fff;
  padding: 2px;
  float:left;
  margin: 2px;
}
.cookList li span{
  display: block;
  float:left;
}
.foodImg{
  width: 40%;
}
.foodName{
  font-size: 18px;
  padding-left: 10px;
  color:brown;
}
.foodPrice{
  font-size: 16px;
  padding-left: 10px;
  padding-top:10px;
  width: 40%;
  text-align: right;
}
.totalDiv{
  background: #fff;
  padding: 10px;
  border-bottom: 1px solid #d3dce6;
}
</style>
