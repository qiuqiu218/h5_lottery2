<template>
  

  <!-- <div v-if="show" :class="'so-right '+ (show?'active':'')"> -->
    <div v-if="show" :class="'so-right '+ (show?'active':'')">
        <!--<div>
            <img src="/static/frist/images/top/zoushi.png">
        </div>-->
        <div class="so-shade" @click="close"></div>
        <div @click="close">
            <div class="right_menu_box" v-if="show">
                <ul class="right_menu">
                    <li class="r_record">
                        <!-- <router-link :to="(lotteryid =='10') ? '/lhc/LhcBetRecord' : '/publicTemplate/betRecord'"> -->
                        <!-- <a href = '/lhc/LhcBetRecord' > -->
                          <router-link :to=" '/lhc/LhcBetRecord' ">
                            <p><span class="icon icon_r_record"></span>投注记录</p>
                          </router-link>
                        <!-- </a> -->
                    </li>
                    <li class="r_pastview">
                        <router-link to="/publicTemplate/pastView">
                            <p><span class="icon icon_r_pastview"></span>往期开奖</p>
                        </router-link>
                    </li>
                    <!--<li class="r_roadbeads" v-if="lotteryid =='8'"> &lt;!&ndash; 北京pk10 &ndash;&gt;
                        <router-link to="/publicTemplate/pk10roadBeads">
                            <p>路珠</p>
                        </router-link>
                    </li>-->
                    <li class="r_roadbeads" v-if=" (lotteryid != '10')&&(lotteryid != '110')&&(lotteryid != '116')&&(lotteryid != '118') ">
                        <router-link to="/publicTemplate/roadBeads">
                            <p><span class="icon icon_r_roadbeads"></span>路珠</p>
                        </router-link>
                    </li>
                    <li class="r_long" v-if=" (lotteryid != '116')&&(lotteryid != '118')">
                        <router-link to="/publicTemplate/dsLong">
                            <p><span class="icon icon_r_long"></span>双面长龙</p>
                        </router-link>
                    </li>
                    <li class="play " @click="play">
                        <!-- <img src="/static/frist/images/right/5.png"> -->
                        <p><span class="icon icon_r_play"></span>玩法说明</p>
                    </li>
                    <li class="r_today">
                        <!-- <img src="/static/frist/images/right/6.png"> -->
                        <p v-if="lotteryid == 10">
                            <span class="icon icon_w_record"></span>本周输赢
                        </p>
                        <p v-else>
                            <span class="icon icon_w_record"></span>今日输赢
                        </p>
                       <!-- <div :class="'today_payoff '+ (payoff>=0?' win_payoff':'lose_payoff')">({{(payoff>=0?'+':'')}}{{fortMoney(roundAmt(payoff))}})</div>-->
                        <div class="today_payoff win_payoff" v-if="payoff>=0">+{{fortMoney(roundAmt(payoff))}}</div>
                        <div class="today_payoff lose_payoff" v-else>-{{fortMoney(roundAmt(payoff).toString().replace(/-/g,''))}}</div>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>


<script>
import Mixin from '@/Mixin'

// import $ from "jquery";

export default {
  name: 'UserMenu',
  mixins:[Mixin],
  props:['el', 'payoff'],
  data :function() {
        return {
            show:false ,
            lotteryid :this.$parent.lotteryID , // 彩种 id
        }
    },
  mounted:function() {
    $(this.el).on('click', (e)=>{
      this.show = true;
      e.preventDefault()
    })
  },
  methods:{
    play:function(e){
        this.$emit('play')
    },
    close:function(e){
      this.show = false;
    }
  },
}
</script>
<style scoped>
  .so-shade { display: block; z-index: 0; height: 100% !important; }
  .so-right > div:last-child > div { display: block; }
  .right_menu a{
      display: inline-block;
      width: 100%;
  }
</style>