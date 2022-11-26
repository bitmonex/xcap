<template>
  <div class="coin">
    <div class="title" @click.stop="openDetails">
        <span :style="{ backgroundImage : 'url('+ iconbase +')' }"></span>
        <i class="tiker">{{info.base}}/{{info.quote}}</i>
        <i class="pv">{{ticker.price || '' }}<u class="hide">{{info.quote}}</u></i>
        <Sparkline :cdata="ticker.price" class="min" v-if="ticker.price" />
        <div class="price" :class="[(ticker.percent < 0)?'down':'up']" v-if="ticker.price"><b class="ch">{{ ticker.percent }}%</b><i class="indication"></i></div>
        <i class="vol">Vol<b>{{ticker.vol}}</b></i>
        <i class="val">Value<b :class="[(ticker.percent < 0)?'down':'up']" v-if="ticker.price">{{parseFloat(ticker.chg).toFixed((info.quote === 'USDT') ? 3 : 8)}}</b></i>
    </div>
    <i class="rem" @click="removeCard"><i><u>close</u><b>&plus;</b></i></i>
    <Graph />
  </div>
</template>

<script>
    import Sparkline from './Sparkline.vue'
    import Graph from './Graph.vue'
    import {unSubscribeSymbol} from '../services/binance'
    export default {
        props: ['ticker', 'info'],
        computed: {
            iconbase() {
                return `https://s2.coinmarketcap.com/static/img/coins/64x64/${this.info.cid}.png`
            }
        },
        methods: {
          removeCard() {
            unSubscribeSymbol(this.info.symbol);
            this.$store.commit('REMOVE_COIN_PAIR', this.info.symbol)
          },
          openDetails() {
            this.$router.push({name: 'infoview', params: { 'symbol': this.info.symbol }})
          }
        },
        components: {Sparkline,Graph}
    }
</script>

<style scoped>
    .coin{float:left; width:calc(100% /2); position:relative}

    .title{float:left; height:50px; cursor:pointer}
    .tiker,.coin .pv,.coin .vol,.rem,.min,.price,.vol,.val{position:absolute}
    .tiker{top:4px; left:50px; color:#777; cursor:pointer}
    .pv{top:24px; left:50px; color:#ccc; font-weight:bold; font-size:1.1em}
    .pv u{text-decoration:none; font-size:9px; color:#444; position:relative; top:-1px; left:3px;}
    .coin span{float:left; height: 34px; width: 34px; background-position: 0 0; background-size: 100% 100%; border-radius: 50%; margin:8px 0 0 8px;}

    .price{top:9px; left:145px;text-shadow: 2px 2px 2px #000;}
    .price i{float:left; margin-top:11px}
    .price .ch{float:left; width:65px; margin:6px 7px 0 0; font-size:1.1em; text-align:right}

    .vol,.val{color:#777; font-size:.8em}
    .vol b,.val b{margin-left:5px;}
    .vol b{color:#ccc;}
    .vol{top:9px; right:11px;}
    .val{top:26px; right:11px;}

    .rem{top:58px; right:9px; font-family:'Avenir'; cursor:pointer}
    .rem i{display:block; width:26px; height:26px; border-radius:35px; position:relative;}
    .rem b,.rem u{position:absolute; color:#777}
    .rem u{display:none; top:4px; right:32px; font-size:.9em}
    .rem b{top:-7px; right:3px; display:block; transform: rotate(45deg); color:#999; font-size:2.2em; font-weight:normal}
    .rem:hover i{background:#000}
    .rem:hover b,.rem:hover u{color:#fff}
    .rem:hover u{display:block}

    .min{top:7px; right:140px; width:100px;}
    .graph{clear:both; display:none; height:400px; border:1px solid #333; background:#111; color:#777; text-align: center;}
</style>
