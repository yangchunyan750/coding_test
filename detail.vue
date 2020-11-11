<template>
    <div class="view_list">
        <ul class="container">
            <li class="info" v-for="(item,index) in info" :key="index">
                <div class="info_num_date">
                    <span class="info_num">编号：{{item.num}}</span>
                    <span class="info_date">时间：{{item.date}}</span>
                </div>
                <div class="info_details" @click.stop="gotoDetail()">查看详情<van-icon name="arrow" /></div>
            </li>
        </ul>
    </div>
</template>

<script>
  export default {
    name: "ContentList",
    // props:{
    //   info:{
    //     type:Object,
    //     default: null
    //   }
    // },
    data(){
      return {
        info:[
          {
            num:'2020202',
            date:'2020-11-02'
          },
          {
            num:'2020202',
            date:'2020-11-02'
          },
          {
            num:'2020202',
            date:'2020-11-02'
          }
        ]
      }
    },
    methods:{
      // 点击进入详情页面
      gotoDetail(){
        this.$router.push("/peopleInfo")
      }
    }
  };
</script>

<style lang='scss' scoped>
.view_list {
    .container {
        background: #F6F6F6;
        width: 100vw;
        height: 100vh;
        display: flex;
        display: -webkit-flex;
        flex-direction: column;
        align-items: center;

        .info {
            width: 93.6vw;
            background: #ffffff;
            margin-top: 20px;
            -webkit-border-radius: 15;
            -moz-border-radius: 15;
            border-radius: 15;
            box-shadow: 0px 4px 10px 0px rgba(0, 0, 0, 0.01);
            display: flex;
            padding: 15px 10px;
            box-sizing: border-box;
            justify-content: space-between;
            flex-shrink: 0;

            .info_num_date {
                display: flex;
                margin-left: 10px;
                flex-direction: column;
                justify-content: space-around;

                .info_num {
                    color: #333333;
                    font-size: 20px;
                    font-wight: Medium;
                }
                .info_date {
                    color: #CCCCCC;
                    font-size: 16px;

                }
            }

            .info_details{
                color:#CCCCCC;
                font-size:16px;
                display: flex;
                align-items: center;
            }
        }
    }
}
</style>