<template>
    <div class="order-confirm">
      <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" style="position: absolute; width: 0px; height: 0px; overflow: hidden;">
      </svg>
      <div class="wrapper">
        <div class="container">
          <div class="order-box">
            <div class="item-address">
              <h2 class="addr-title">收货地址</h2>
              <div class="addr-list clearfix">
                <div class="addr-info" v-for="(item,index) in list" :key="index">
                  <h2>{{item.receiverName}}</h2>
                  <div class="phone">{{item.receiverMobile}}</div>
                  <div class="street">{{item.receiverProvince+' '+item.receiverCity+' '+item.receiverDistrict+' '+item.receiverAddress}}</div>
                  <div class="action">
                    <a href="javascipt:;" class="fl">

                      <svg class="icon icon-del">
                        <use xlink:href="#icon-del"></use>
                      </svg>
                    </a>
                     <a href="javascipt:;" class="fr">
                      <svg class="icon icon-edit">
                        <use xlink:href="#icon-edit"></use>
                      </svg>
                    </a>
                  </div>
                </div>
                 <div class="addr-add">
                   <div class="icon-add"></div>
                   <div>添加新地址</div>
                 </div>
              </div>
            </div>
            <div class="item-good">
              <h2>商品</h2>
              <ul>
                <li v-for="(item,index) in cartList" :key="index">
                  <div class="good-name">
                    <img v-lazy="item.productMainImage" alt=""/>
                    <span>{{item.productName+' '+item.productSubtitle}}</span>
                  </div>
                  <div class="good-price">{{item.productPrice}}元×{{item.quantity}}</div>
                  <div class="good-total">{{item.productTotalPrice}}元</div>
                </li>
              </ul>
            </div>
            <div class="item-shipping">
              <h2>配送方式</h2>
              <span>包邮</span>
            </div>
            <div class="item-invoice">
              <h2>发票</h2>
              <a href="javascript:;">电子发票</a>
              <a href="javascript:;">个人</a>
            </div>
            <div class="detail">
              <div class="item">
                <span class="item-name">商品件数:</span>
                <span class="item-val">{{count}}件</span>
              </div>
              <div class="item">
                 <span class="item-name">商品总价:</span>
                 <span class="item-val">{{cartTotalPrice}}元</span>
              </div>
              <div class="item">
                <span class="item-name">优惠活动:</span>
                <span class="item-val">0元</span>
              </div>
              <div class="item">
                <span class="item-name">运费:</span>
                <span class="item-val">0元</span>
              </div>
              <div class="item-total">
                 <span class="item-name">应付总额:</span>
                 <span class="item-val">{{cartTotalPrice}}元</span>
              </div>
            </div>
            <div class="btn-group">
              <a href="/#/cart" class="btn btn-default btn-large">返回购物车</a>
              <a href="javascript:;" class="btn btn-large">去结算</a>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>
<script>
export default{
    name:'order-confirm',
    data(){
      return{
      list:[],//收货地址列表
      cartList:[],//购物车中需要结算的商品列表
      cartTotalPrice:0,//商品总金额
      count:0,//商品结算数量
    }
    },
    mounted(){
     this,this.getAddressList();
     this.getCartList();
    },
    methods:{
      getAddressList(){
         this.axios.get('/shippings').then((res)=>{
           this.list=res.list;
         })
      },
      getCartList(){
         this.axios.get('/carts').then((res)=>{
           let list=res.cartProductVoList;//获取购物车中所有的商品数据
          this.cartTotalPrice=res.cartTotalPrice;//商品总金额
          this.cartList=list.filter(item=>item.productSelected);
          this.cartList.map((item)=>{
            this.count+=item.quantity;
          })
         })
      }
    }
}
</script>
<style lang="scss">
 .order-confirm {
  .wrapper {
    background-color: #f5f5f5;
    padding-top: 30px;
    padding-bottom: 84px;
    .order-box {
      background-color: #ffffff;
      padding-left: 40px;
      padding-bottom: 40px;
      .addr-title {
        font-size: 20px;
        color: #333333;
        font-weight: 200;
        margin-bottom: 21px;
      }
      .item-address {
        padding-top: 38px;
        .addr-list {
          .addr-info,
          .addr-add {
            box-sizing: border-box;
            float: left;
            width: 271px;
            height: 180px;
            border: 1px solid #e5e5e5;
            margin-right: 15px;
            padding: 15px 24px;
            font-size: 14px;
            color: #757575;
          }
          .addr-info {
            cursor: pointer;
            h2 {
              height: 27px;
              font-size: 18px;
              font-weight: 300;
              color: #333;
              margin-bottom: 10px;
            }
            .street {
              height: 50px;
            }
            .action {
              height: 50px;
              line-height: 50px;
              .icon {
                width: 20px;
                height: 20px;
                fill: #666666;
                vertical-align: middle;
                &:hover {
                  fill: #ff6700;
                }
              }
            }
            &.checked {
              border: 1px solid #ff6700;
            }
          }
          .addr-add {
            text-align: center;
            color: #999999;
            cursor: pointer;
            .icon-add {
              width: 30px;
              height: 30px;
              border-radius: 50%;
              background: url("/imgs/icon-add.png") #e0e0e0 no-repeat center;
              background-size: 14px;
              margin: 0 auto;
              margin-top: 45px;
              margin-bottom: 10px;
            }
          }
        }
      }
      .item-good {
        margin-top: 34px;
        border-bottom: 1px solid #e5e5e5;
        padding-bottom: 12px;
        h2 {
          border-bottom: 1px solid #e5e5e5;
          padding-bottom: 5px;
        }
        li {
          display: flex;
          align-items: center;
          height: 40px;
          line-height: 40px;
          margin-top: 10px;
          font-size: 16px;
          color: #333333;
          .good-name {
            flex: 5;
            img {
              width: 30px;
              height: 30px;
              vertical-align: middle;
            }
          }
          .good-price {
            flex: 2;
          }
          .good-total {
            padding-right: 44px;
            color: #ff6600;
          }
        }
      }
      .item-shipping,
      .item-invoice {
        margin-top: 31px;
        line-height: 20px;
        h2 {
          display: inline-block;
          margin-right: 71px;
          font-size: 20px;
          width: 80px;
        }
        span,
        a {
          font-size: 16px;
          color: #ff6700;
          margin-right: 23px;
        }
      }
      .detail {
        padding: 50px 44px 33px 0;
        border-bottom: 1px solid #f5f5f5;
        text-align: right;
        font-size: 16px;
        color: #666666;
        .item-val {
          color: #ff6700;
        }
        .item {
          line-height: 15px;
          margin-bottom: 12px;
        }
        .item-val {
          display: inline-block;
          width: 100px;
        }
        .item-total {
          .item-val {
            font-size: 28px;
          }
        }
      }
      .btn-group {
        margin-top: 37px;
        text-align: right;
      }
    }
  }
  .edit-wrap {
    font-size: 14px;
    .item {
      margin-bottom: 15px;
      .input {
        display: inline-block;
        width: 283px;
        height: 40px;
        line-height: 40px;
        padding-left: 15px;
        border: 1px solid #e5e5e5;
        & + .input {
          margin-left: 14px;
        }
      }
      select {
        height: 40px;
        line-height: 40px;
        border: 1px solid #e5e5e5;
        margin-right: 15px;
      }
      textarea {
        height: 62px;
        width: 100%;
        padding: 13px 15px;
        box-sizing: border-box;
        border: 1px solid #e5e5e5;
      }
    }
  }
}
</style>
