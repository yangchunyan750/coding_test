<template>
  <div class="appoint_card">
    <div class="card_commen">
      <div class="card_title">
        <span class="title_left">{{card.yymc || ''}}</span>
        <span class="title_right">{{card.statusText || ''}}</span>
      </div>
      <div class="card_middle">
        <span class="middle_hos">{{card.yqmc || ''}}</span>
        <span class="middle_dept">{{card.ksmc || ''}}</span>
      </div>
      <div class="card_time">
        <span class="one_time">{{card.date}}</span>
        <span class="one_time">{{card.week}}</span>
        <span class="one_time">{{card.ptype}}</span>
        <span class="one_time">{{card.yysd}}</span>
      </div>
    </div>
    <div class="card_cancel" v-show="(card.status === 'NORMAL') || (card.status === 'FAILED')" v-if="flag">
      <div class="cancel" v-if="card.status === 'NORMAL'">
        <van-button type="default" round @click.stop="onCancel" :loading="card.loadBtn" loading-type="spinner" loading-text="取消预约中...">取消预约</van-button>
      </div>
      <div class="cancel reappoint" v-else-if="card.status === 'FAILED'">
        <van-button type="info" plain round @click.stop="reAppoint(card.yydm)">重新预约</van-button>
      </div>
    </div>
  </div>
</template>

<script>
  import moment from 'moment'
  import { Toast } from 'vant'
  export default {
  name: 'AppointCard',
  fitlers: {
    emptyString(value) {
      return value || ''
    }
  },
  data(){
    return {
      nowDate : moment() ? moment() : '',//获取当前时间
      nucDate : moment(this.card.date + this.card.yysd.split('-')[0], 'YYYY-MM-DD HH:mm') ? moment(this.card.date + this.card.yysd.split('-')[0], 'YYYY-MM-DD HH:mm') : ''//预约时间
    }
  },
  computed : {
    flag : function(){
      return this.nucDate.isBefore(this.nowDate) ? false : true;
    }
  },
  props: {
    card: Object
  },
  methods: {
    onCancel() {
      let newDate = moment();
      if ( this.nucDate.isBefore(newDate) ) {
         Toast('您已到预约时间，无法取消预约')
      } else {
        this.$emit('on-cancel', this.card || '')
      }
    },
    reAppoint(data) {
      this.$router.push({path: '/nucleic-sample/appoint', query: {oid: data}})
    }
  }
}
</script>

<style lang='scss' scoped>
.appoint_card {
  width: 92%;
  margin: 0 4%;
  margin-top: 18px;
  border-radius: 5px;
  background: #ffffff;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  .card_commen {
    height: 110px;
    padding: 15px;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

    .card_title {
      display: flex;
      align-items: center;
      justify-content: space-between;

      .title_left {
        font-size: 16px;
      }

      .title_right {
        color: #999999;
      }
    }

    .card_middle {
      .middle_dept {
        margin-left: 10px;
      }
    }

    .card_time {
      .one_time {
        margin-right: 10px;
      }
    }
  }

  .card_cancel {
    width: 100%;
    height: 50px;
    padding-left: 15px;
    box-sizing: border-box;

    .cancel {
      width: 100%;
      height: 100%;
      padding-right: 15px;
      box-sizing: border-box;
      border-top: 1px dashed #dddddd;
      display: flex;
      justify-content: flex-end;
      align-items: center;
      >button {
        // width: 100px;
        height: auto;
        padding: 0;
        >span {
          padding: 8px 14px;
          font-size: 15px;
          color: #999999;
        }
      }
      .van-button--loading {
        .van-button__loading {
          width: 17px;
          height: 17px;
          margin-left: 5px;
        }
        .van-button__text {
          padding-left: 0;
        }
      }
    }

    .reappoint {
      >button {
        >span {
          color: #2A8BFF;
        }
      }
    }
  }
}
</style>
