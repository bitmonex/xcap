<template>
    <div class="head">

        <div class="cmd" :class="{show: cmdOpen}">
            <b>Tiker:<i></i></b>
            <b>Timeframe:<i id=timeframe></i></b>
            <b>Timezone:<i id=timezone></i></b>
            <b>Indicator:<i id="indicator"></i></b>
            <b>Style:<i id="style"></i></b>
            <b>W: <i>2</i></b>
            <b>H: <i>2</i></b>
            <br>
            <b>Settings:<i id="setting"></i> <i>54<u>er</u></i></b>
        </div>
        <div class="setting">
            <i @click="settingOpen = !settingOpen" :class="{on: settingOpen}">Settings<u></u></i>
            <div class="drop" :class="{show: settingOpen}">
                <label v-for="setting of settings" :key="setting.data">{{setting.title}}<input type="checkbox"></label>
                <label @change="cmdOpen = !cmdOpen" :class="{on: cmdOpen}">Show Console<input type="checkbox"></label>
            </div>
        </div>
        <div class="timezone">
            <i @click="timezoneOpen = !timezoneOpen" :class="{on: timezoneOpen}">(UTC+13:45) Chatham Islands<u></u></i>
            <div class="drop" :class="{show: timezoneOpen}">
                <a v-for="timezone of timezones" :key="timezone.data">{{timezone.title}}</a>
            </div>
        </div>
        <span><a v-for="menu in menus" :key="menu.title" :href="menu.url" :class="{logo: menu.logo}">{{menu.title}}</a></span>
        <div class="filter">
            <div class="sizer">
                <b>Layout</b>
                <input id="wsize" type="number" value="1" min="1" max="8" />
                <input id="hsize" type="number" value="1" min="1" max="8" />
            </div>
            <div class="style">
                <b>Style</b>
                <i @click="styleOpen = !styleOpen" :class="{on: styleOpen}">Bars<u></u></i>
                <div class="drop" :class="{show: styleOpen}">
                    <a v-for="style in styles" :key="style.data">{{style.title}}</a>
                </div>
            </div>
            <div class="indicator">
                <b>Indicators</b>
                <i  @click="indicatorOpen = !indicatorOpen" :class="{on: indicatorOpen}">Indicators<u></u></i>
                <div class="drop" :class="{show: indicatorOpen}">
                    <label v-for="indicator in indicators" :key="indicator.data">{{indicator.title}}<input type="checkbox"></label>
                </div>
            </div>
            <div class="timeframe">
                <b>Timeframes</b>
                <a v-for="timeframe in timeframes" :key="timeframe.data">{{timeframe.title}}</a>
            </div>
            <div class="tiker">
                <b>Tikers</b>
                <input type="text" id="tiker" value="BTCUSDTPERP,ETHUSDTPERP,TRBUSDTPERP" autocomplete="off"/>
                <a>Go</a>
            </div>
        </div>
    </div>
</template>

<script>
export default{
    data(){
        return{
            settings:[
                {title: 'Show Drawing Tools Bar', data: 'Show Drawing Tools Bar', status: false},
                {title: 'Show Top Toolbar', data: 'Show Top Toolbar', status: false},
                {title: 'Show Bottom Toolbar', data: 'Show Bottom Toolbar', status: false},
                {title: 'Show Details', data: 'Show Details', status: false},
                {title: '«Get Image» button', data: '«Get Image» button', status: false},
                {title: 'Enable Publishing', data: 'Enable Publishing', status: false},
                {title: 'Allow Symbol Change', data: 'Allow Symbol Change', status: false},
                {title: 'Show Console', data: 'Show Console', status: false},
                {title: 'Custom Tiker', data: 'Custom Tiker', status: false}
            ],
            timezones:[
                {title: 'UTC', data: 'Etc/UTC', status: true},
                {title: '(UTC-10) Honolulu', data: 'Pacific/Honolulu', status: false},
                {title: '(UTC-8) Los Angeles', data: 'America/Los_Angeles', status: false},
                {title: '(UTC-7) Phoenix', data: 'America/Phoenix', status: false},
                {title: '(UTC-6) Mexico City', data: 'America/Mexico_City', status: false},
                {title: '(UTC-5) Bogota', data: 'America/Bogota', status: false},
                {title: '(UTC-5) New York', data: 'America/New_York', status: false},
                {title: '(UTC-4) Caracas', data: 'America/Caracas', status: false},
                {title: '(UTC-3) Buenos Aires', data: 'America/Argentina/Buenos_Aires', status: false},
                {title: '(UTC-2) Sao Paulo', data: 'America/Sao_Paulo', status: false},
                {title: '(UTC) London', data: 'Europe/London', status: false},
                {title: '(UTC+1) Rome', data: 'Europe/Rome', status: false},
                {title: '(UTC+2) Jerusalem', data: 'Asia/Jerusalem', status: false},
                {title: '(UTC+3) Istanbul', data: 'Europe/Istanbul', status: false},
                {title: '(UTC+3:30) Tehran', data: 'Asia/Tehran', status: false},
                {title: '(UTC+4) Dubai', data: 'Asia/Dubai', status: false},
                {title: '(UTC+5) Ashkhabad', data: 'Asia/Ashkhabad', status: false},
                {title: '(UTC+5:30) Kolkata', data: 'Asia/Kolkata', status: false},
                {title: '(UTC+6) Almaty', data: 'Asia/Almaty', status: false},
                {title: '(UTC+7) Bangkok', data: 'Asia/Bangkok', status: false},
                {title: '(UTC+8) Taipei', data: 'Asia/Taipei', status: false},
                {title: '(UTC+8) Singapore', data: 'Asia/Singapore', status: false},
                {title: '(UTC+8) Shanghai', data: 'Asia/Shanghai', status: false},
                {title: '(UTC+8) Chongqing', data: 'Asia/Chongqing', status: false},
                {title: '(UTC+8) Hong Kong', data: 'Asia/Hong_Kong', status: false},
                {title: '(UTC+9) Seoul', data: 'Asia/Seoul', status: false},
                {title: '(UTC+9) Tokyo', data: 'Asia/Tokyo', status: false},
                {title: '(UTC+10) Brisbane', data: 'Australia/Brisbane', status: false},
                {title: '(UTC+10:30) Adelaide', data: 'Australia/Adelaide', status: false},
                {title: '(UTC+11) Sydney', data: 'Australia/Sydney', status: false},
                {title: '(UTC+13) New Zealand', data: 'Pacific/Auckland', status: false},
                {title: '(UTC+13) Tokelau', data: 'Pacific/Fakaofo', status: false},
                {title: '(UTC+13:45) Chatham Islands', data: 'Pacific/Chatham', status: false}
            ],
            menus:[
                {title: 'xcap', url: '/', status: true, logo: true},
                {title: 'Screener', url: '/screener', status: true},
                {title: 'Market', url: '/market', status: true},
                {title: 'Features', url: '/features', status: true}
            ],
            styles:[
                {title: 'Bars', data: '0', status: false},
                {title: 'Candles', data: '1', status: false},
                {title: 'Line', data: '2', status: false},
                {title: 'Area', data: '3', status: false},
                {title: 'Renko', data: '4', status: false},
                {title: 'Kagi', data: '5', status: false},
                {title: 'Point and Figure', data: '6', status: false},
                {title: 'Line Break', data: '7', status: false},
                {title: 'Heikin Ashi', data: '8', status: false},
                {title: 'Hollow Candles', data: '9', status: false}
            ],
            indicators:[
                {title: 'ACCD', data: 'ACCD', status: false},
                {title: 'studyADR', data: 'studyADR', status: false},
                {title: 'AROON', data: 'AROON', status: false},
                {title: 'ATR', data: 'ATR', status: false},
                {title: 'AwesomeOscillator', data: 'AwesomeOscillator', status: false},
                {title: 'BB', data: 'BB', status: false},
                {title: 'BollingerBandsR', data: 'BollingerBandsR', status: false},
                {title: 'BollingerBandsWidth', data: 'BollingerBandsWidth', status: false},
                {title: 'CMF', data: 'CMF', status: false},
                {title: 'ChaikinOscillator', data: 'ChaikinOscillator', status: false},
                {title: 'chandeMO', data: 'chandeMO', status: false},
                {title: 'ChoppinessIndex', data: 'ChoppinessIndex', status: false},
                {title: 'CCI', data: 'CCI', status: false},
                {title: 'CRSI', data: 'CRSI', status: false},
                {title: 'CorrelationCoefficient', data: 'CorrelationCoefficient', status: false},
                {title: 'DetrendedPriceOscillator', data: 'DetrendedPriceOscillator', status: false},
                {title: 'DM', data: 'DM', status: false},
                {title: 'DONCH', data: 'DONCH', status: false},
                {title: 'DoubleEMA', data: 'DoubleEMA', status: false},
                {title: 'EaseOfMovement', data: 'EaseOfMovement', status: false},
                {title: 'EFI', data: 'EFI', status: false},
                {title: 'ENV', data: 'ENV', status: false},
                {title: 'FisherTransform', data: 'FisherTransform', status: false},
                {title: 'HV', data: 'HV', status: false},
                {title: 'hullMA', data: 'hullMA', status: false},
                {title: 'IchimokuCloud', data: 'IchimokuCloud', status: false},
                {title: 'KLTNR', data: 'KLTNR', status: false},
                {title: 'KST', data: 'KST', status: false},
                {title: 'LinearRegression', data: 'LinearRegression', status: false},
                {title: 'MACD', data: 'MACD', status: false},
                {title: 'MOM', data: 'MOM', status: false},
                {title: 'MF', data: 'MF', status: false},
                {title: 'MoonPhases', data: 'MoonPhases', status: false},
                {title: 'MASimple', data: 'MASimple', status: false},
                {title: 'MAExp', data: 'MAExp', status: false},
                {title: 'MAWeighted', data: 'MAWeighted', status: false},
                {title: 'OBV', data: 'OBV', status: false},
                {title: 'PSAR', data: 'PSAR', status: false},
                {title: 'PivotPointsHighLow', data: 'PivotPointsHighLow', status: false},
                {title: 'PivotPointsStandard', data: 'PivotPointsStandard', status: false},
                {title: 'PriceOsc', data: 'PriceOsc', status: false},
                {title: 'PriceVolumeTrend', data: 'PriceVolumeTrend', status: false},
                {title: 'ROC', data: 'ROC', status: false},
                {title: 'RSI', data: 'RSI', status: false},
                {title: 'VigorIndex', data: 'VigorIndex', status: false},
                {title: 'VolatilityIndex', data: 'VolatilityIndex', status: false},
                {title: 'SMIErgodicIndicator', data: 'SMIErgodicIndicator', status: false},
                {title: 'SMIErgodicOscillator', data: 'SMIErgodicOscillator', status: false},
                {title: 'Stochastic', data: 'Stochastic', status: false},
                {title: 'StochasticRSI', data: 'StochasticRSI', status: false},
                {title: 'TripleEMA', data: 'TripleEMA', status: false},
                {title: 'Trix', data: 'Trix', status: false},
                {title: 'UltimateOsc', data: 'UltimateOsc', status: false},
                {title: 'VSTOP', data: 'VSTOP', status: false},
                {title: 'Volume', data: 'Volume', status: false},
                {title: 'VWAP', data: 'VWAP', status: false},
                {title: 'MAVolumeWeighted', data: 'MAVolumeWeighted', status: false},
                {title: 'WilliamR', data: 'WilliamR', status: false},
                {title: 'WilliamsAlligator', data: 'WilliamsAlligator', status: false},
                {title: 'WilliamsFractal', data: 'WilliamsFractal', status: false},
                {title: 'ZigZag', data: 'ZigZag', status: false}
            ],
            timeframes:[
                {title: '5m', data: '5', status: false},
                {title: '15m', data: '15', status: false},
                {title: '30m', data: '30', status: false},
                {title: '1h', data: '60', status: true},
                {title: '4h', data: '240', status: false},
                {title: 'D', data: 'D', status: false},
                {title: 'W', data: 'W', status: false}
            ],
            settingOpen: false,
            timezoneOpen: false,
            styleOpen: false,
            indicatorOpen: false,
            cmdOpen: false

        }
    }
}
</script>

<style>

</style>
