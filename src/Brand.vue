
<template>
  <div class="brand-container">
  	<div class="wrap">
      <header>
        <div class="weather">
          <img :src="imgSrc">
<!--          <span class="tem">{{ weatcherData.tem }}°C</span> -->
          <span class="wea">{{ weatcherData.wea }}</span>
        </div>
        <h2>San Francisco Crime Data Analysis</h2>
        <div class="showTime">
          <span class="time">{{ nowTime }}</span>
          <span class="date">
            <span>{{ week }}</span>
            <span>{{ date }}</span>
          </span>
        </div>
      </header>

      <section class="mainbox">
        <div class="item left">
          <div class="panel">
            <h2>Annual Total Crime Count</h2>
            <business :area="selectedArea" />
            <div class="panel-footer"></div>
          </div>
          <div class="panel">
            <h2>Crime Type</h2>
            <talent :area="selectedArea" />
            <div class="panel-footer"></div>
          </div>
          <div class="panel">
            <h2>Daily Crime Count</h2>
            <income :area="selectedArea" />
            <div class="panel-footer"></div>
          </div>
        </div>

        <div class="item center">
          <div class="resume">
            <div class="resume-hd">
              <ul>
                <li>
                  <countTo :startVal='startVal' :endVal='endVals[0]' :duration='1000' separator=""></countTo>
                </li>
                <li>
                  <countTo :startVal='startVal' :endVal='endVals[1]' :duration='1000' separator=""></countTo>
                </li>
                <li>
                  <countTo :startVal='startVal' :endVal='endVals[2]' :duration='1000' separator=""></countTo>
                </li>
              </ul>
            </div>
            <div class="resume-bd">
              <ul>
                <li>Total Crime Count</li>
                <li>Proportion of Resolved Incidents</li>
                <li>Unresolved Incidents</li>
              </ul>
            </div>
          </div>
          <div class="map">
            <div id="map"></div>
          </div>
        </div>

        <div class="item right">
          <div class="panel">
            <h2>Resolved Incidents</h2>
            <wordCloud :area="selectedArea" />
            <div class="panel-footer"></div>
          </div>
          <div class="panel">
            <h2>Weekly Distribution</h2>
            <distribution :area="selectedArea" />
            <div class="panel-footer"></div>
          </div>
          <div class="panel">
            <history :area="selectedArea" />
            <div class="panel-footer"></div>
          </div>
        </div>
      </section>
  
    </div>
    
  </div>
</template>
<script>
import '@/assets/js/flexible'
import countTo from 'vue-count-to'
import L from 'leaflet';
import 'leaflet/dist/leaflet.css';
import { nextTick } from 'vue';
export default {
  name: 'Brand',
  components: {
    countTo
  },
  data() {
  	return {
      endVals: [0, 0, 0],
      endValData: {
        'MISSION': [288985, 43.360728065470525, 163679],
        'BAYVIEW': [205480, 37.627019661280904, 128164],
        'CENTRAL': [221923, 26.419523888916423, 163292],
        'TARAVAL': [155461, 26.868475051620667, 113691],
        'TENDERLOIN': [186954, 62.6250307562288, 69874],
        'INGLESIDE': [181092, 31.51602500386544, 124019],
        'PARK': [119698, 33.053183846012466, 80134],
        'SOUTHERN': [390692, 36.718182097406654, 247237],
        'RICHMOND': [112804, 24.101095705826033, 85617],
        'NORTHERN': [266435, 29.79525963180513, 187050],
        'ALL':[2129525,36.00648031838086,1362758]
      },
      selectedArea: 'ALL',
      nowTime: '',
      week: '',
      date: '',
      timer: null,
      imgSrc: '',
      weatcherData: {},
      startVal: 0,
      geoCoordMap: {},
      XAData: [
        [{ name: "长沙" }, { name: "北京", value: 100 }],
        [{ name: "长沙" }, { name: "上海", value: 100 }],
        [{ name: "长沙" }, { name: "广州", value: 100 }],
        [{ name: "长沙" }, { name: "深圳", value: 100 }],
        [{ name: "长沙" }, { name: "西安", value: 100 }]
      ],
      XNData: [
        [{ name: "长沙" }, { name: "西宁", value: 100 }],
        [{ name: "长沙" }, { name: "拉萨", value: 100 }],
        [{ name: "长沙" }, { name: "哈尔滨", value: 100 }],
        [{ name: "长沙" }, { name: "成都", value: 100 }],
        [{ name: "长沙" }, { name: "重庆", value: 100 }]
      ],
      YCData: [
        [{ name: "北京" }, { name: "长沙", value: 100 }],
        [{ name: "北京" }, { name: "贵阳", value: 100 }],
        [{ name: "北京" }, { name: "杭州", value: 100 }]
      ]

  	}
  },
  computed: {
  	
  },
  created() {
  },
  mounted() {
    this.updateEndVals(this.area);
    this.getWeather();
    this.timer = setInterval(() => {
      this.getWeather();
    }, 1000 * 60 * 60);

    this.nowTimes();

    this.$nextTick(() => {
      this.initializeMap();
    });
  },
  watch: {
    selectedArea(newArea) {
      this.updateEndVals(newArea || 'ALL');
    },
  },
  methods: {
    updateEndVals(newArea) {
      const areaKey = newArea ? newArea.toUpperCase() : 'ALL';
      const endVals = this.endValData[areaKey];
      if (endVals) {
        this.endVals = endVals;
      } else {
        console.warn(`未找到区域 ${areaKey} 的 endVal 数据`);
        this.endVals = [2129525,36.00648031838086,1362758];
      }
    },
    timeFormate(timeStamp) { //显示当前时间
      let newDate = new Date(timeStamp);
      let year = newDate.getFullYear();
      let month = newDate.getMonth() + 1 < 10 ? '0' + (newDate.getMonth() + 1) : newDate.getMonth() + 1;
      let date = newDate.getDate() < 10 ? '0' + newDate.getDate() : newDate.getDate();
      let hh = newDate.getHours() < 10 ? '0' + newDate.getHours() : newDate.getHours();
      let mm = newDate.getMinutes() < 10 ? '0' + newDate.getMinutes() : newDate.getMinutes();
      let ss = newDate.getSeconds() < 10 ? '0' + newDate.getSeconds() : newDate.getSeconds();
      let week = newDate.getDay();
      let weeks = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
      let getWeek =  weeks[week];
      this.week = getWeek;
      this.date = year + '.' + month + '.' + date;
      this.nowTime = hh + ':' + mm + ':' + ss;
    },
    nowTimes() {
      this.timeFormate(new Date());
      setInterval(this.nowTimes, 1000);
      this.clear();
    },
    clear() {
      clearInterval(this.nowTimes)
      this.nowTimes = null;
    },
    getWeather() { // 第三方天气api接口
      axios.get('https://www.tianqiapi.com/api/', {
        params: {
          appid: '26148275',
          appsecret: '2id6H48Y',
          version: 'v6'
        }
      }).then(res => {
        if (res.data) {
          if (res.data.wea_img == 'xue') {
            this.imgSrc = require('../assets/img/brand/xue.png');
          } else if (res.data.wea_img == 'yin') {
            this.imgSrc = require('../assets/img/brand/yin.png');
          } else if (res.data.wea_img == 'yu' || res.data.wea_img == 'bingbao') {
            this.imgSrc = require('../assets/img/brand/yu.png');
          } else if (res.data.wea_img == 'yun') {
            this.imgSrc = require('../assets/img/brand/yun.png');
          } else if (res.data.wea_img == 'wu') {
            this.imgSrc = require('../assets/img/brand/wu.png');
          } else if (res.data.wea_img == 'shachen') {
            this.imgSrc = require('../assets/img/brand/shachen.png');
          } else if (res.data.wea_img == 'lei') {
            this.imgSrc = require('../assets/img/brand/lei.png');
          } else {
            this.imgSrc = require('../assets/img/brand/qing.png');
          }
          this.weatcherData = res.data;
        }
      }).catch(err => {
        console.log(err)
      })
    },
    initializeMap() {
      // 创建地图并设置中心点及缩放等级
      var map = L.map('map',{attributionControl: false}).setView([37.7749, -122.4194], 12);

      // 定义默认样式和高亮样式
      var defaultStyle = {
        color: '#0000ff',
        weight: 3,
        opacity: 1,
        dashArray: '5, 5',
        fillOpacity: 0
      };

      var highlightStyle = {
        weight: 5,
        color: '#ffcc00',
        dashArray: '',
        fillOpacity: 0.3
      };

      // 添加底图图层
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; OpenStreetMap contributors'
      }).addTo(map);

      // 加载 GeoJSON 数据
      fetch('/data/Current Police Districts_20241013.geojson') // 确保文件路径正确
          .then(response => response.json())
          .then(data => {
            L.geoJson(data, {
              style: feature => defaultStyle,
              onEachFeature: (feature, layer) => {
                // 点击事件
                layer.on('click', () => {
                  const areaName = feature.properties.district || feature.properties.NAME || feature.properties.name || 'ALL';
                  this.selectedArea = areaName; // 更新选中的区域
                });

                // 添加标签显示区域名称
                if (feature.properties && feature.properties.district) {
                  layer.bindTooltip(feature.properties.district, {
                    permanent: true,
                    direction: "center",
                    className: "no-background"
                  }).openTooltip();
                }

                // 鼠标悬停高亮显示区域
                layer.on('mouseover', function() {
                  layer.setStyle(highlightStyle);
                });

                // 鼠标移开时恢复原样
                layer.on('mouseout', function() {
                  layer.setStyle(defaultStyle);
                });
              }
            }).addTo(map);
          })
          .catch(error => {
            console.error('加载 GeoJSON 数据时出错:', error);
          });
    },
    // ... 其他方法 ...
  }
}
</script>

<style lang="scss" scoped>
#map {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: 600px; /* 根据需要调整高度 */
  width: 100%;
}
.leaflet-tooltip {
  background: transparent !important;
  border: none !important;
  box-shadow: none !important;
  color: #ff0000;
  font-weight: bold;
  font-size: 12px !important; /* 确保字体大小样式被应用 */
  padding: 0 !important;
}
.brand-container {
  position: absolute;
  width: 100%;
  height: 100%;
  background: #000;
  .wrap {
    background: url(../assets/img/brand/bg.jpg) no-repeat #000;
    background-size: cover;
    line-height: 1.15;
    header {
      position: relative;
      height: 1rem;
      background: url(../assets/img/brand/head_bg.png) no-repeat top center;
      background-size: 100% 100%;
      h2 {
        color: #7ef0ff;
        font-size: 0.475rem;
        text-align: center;
        line-height: 0.75rem;
        letter-spacing: 1px;
      }
      .weather {
        position: absolute;
        left: 1.375rem;
        top: 0.35rem;
        font-size: 0.25rem;
        color: rgba(126, 240, 255, .7);
        img {
          width: .45rem;
        }
        span {
          display: inline-block;
        }
        .tem {
          margin: 0 .1rem 0 .2rem;
        }
      }
      .showTime {
        position: absolute;
        right: 1.375rem;
        top: 0.5rem;
        color: rgba(126, 240, 255, .7);
        display: flex;
        .time {
          font-size: .28rem;
          margin-right: .18rem;
        }
        .date {
          span {
            display: block;
            &:nth-child(1) {
              font-size: .12rem;
              text-align: right;
            }
            &:nth-child(2) {
              font-size: .14rem;
            }
          }
        }
      }
    }
    
    .mainbox {
      min-width: 1024px;
      max-width: 1920px;
      padding: 0.125rem 0.125rem 0;
      display: flex;
      .item {
        flex: 3;
        &.center {
          flex: 5;
          margin: 0 0.125rem 0.1rem;
          overflow: hidden;

          .resume {
            background: rgba(101, 132, 226, 0.1);
            padding: 0.1875rem;
            .resume-hd {
              position: relative;
              border: 1px solid rgba(25, 186, 139, 0.17);
              ul {
                display: flex;
                %li-line {
                  content: "";
                  position: absolute;
                  height: 50%;
                  width: 1px;
                  background: rgba(255, 255, 255, 0.2);
                  top: 25%;
                }
                li {
                  position: relative;
                  flex: 1;
                  text-align: center;
                  height: 1.2rem;
                  line-height: 1.2rem;
                  font-size: 0.65rem;
                  color: #ffeb7b;
                  padding: 0.05rem 0;
                  font-family: 'DIGITALDREAMFAT';
                  font-weight: bold;
                  &:nth-child(2) {
                    &:after {
                      @extend %li-line;
                      right: 0;
                    }
                    &:before {
                      @extend %li-line;
                      left: 0;
                    }
                  }
                }
              }
              &:before {
                content: "";
                position: absolute;
                width: 30px;
                height: 10px;
                border-top: 2px solid #02a6b5;
                border-left: 2px solid #02a6b5;
                top: 0;
                left: 0;
              }
              &:after {
                content: "";
                position: absolute;
                width: 30px;
                height: 10px;
                border-bottom: 2px solid #02a6b5;
                border-right: 2px solid #02a6b5;
                right: 0;
                bottom: 0;
              }
            }
            .resume-bd {
              ul {
                display: flex;
                li {
                  flex: 1;
                  height: 0.5rem;
                  line-height: 0.5rem;
                  text-align: center;
                  font-size: 0.225rem;
                  color: rgba(255, 255, 255, 0.7);
                  padding-top: 0.125rem;
                }
              }
            }
          }
        }
        
        %map-style {
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          width: 6.475rem;
          height: 6.475rem;
          background: url(../assets/img/brand/map.png) no-repeat;
          background-size: 100% 100%;
          opacity: 0.3;
        }
        .map {
          position: relative;
          height: 10.125rem;
          .chart {
            position: absolute;
            top: 0;
            left: 0;
            z-index: 5;
            height: 10.125rem;
            width: 100%;
          }
          .map1 {
            @extend %map-style;
          }
          .map2 {
            @extend %map-style;
            width: 8.0375rem;
            height: 8.0375rem;
            background-image: url(../assets/img/brand/lbx.png);
            opacity: 0.6;
            -webkit-animation: rotate 15s linear infinite;
            animation: rotate 15s linear infinite;
            z-index: 2;
          }
          .map3 {
            @extend %map-style;
            width: 7.075rem;
            height: 7.075rem;
            background-image: url(../assets/img/brand/jt.png);
            -webkit-animation: rotate1 10s linear infinite;
            animation: rotate1 10s linear infinite;
          }
        }
        .panel {
          position: relative;
          height: 3.875rem;
          border: 1px solid rgba(25, 186, 139, 0.17);
          background: rgba(255, 255, 255, 0.04) url(../assets/img/brand/line.png);
          padding: 0 0.1875rem 0;
          margin-bottom: 0.1875rem;
          &:before {
            position: absolute;
            top: 0;
            left: 0;
            content: "";
            width: 10px;
            height: 10px;
            border-top: 2px solid #02a6b5;
            border-left: 2px solid #02a6b5;
          }
          &:after {
            position: absolute;
            top: 0;
            right: 0;
            content: "";
            width: 10px;
            height: 10px;
            border-top: 2px solid #02a6b5;
            border-right: 2px solid #02a6b5;
          }

          .panel-footer {
            position: absolute;
            left: 0;
            bottom: 0;
            width: 100%;
            &:before {
              position: absolute;
              bottom: 0;
              left: 0;
              content: "";
              width: 10px;
              height: 10px;
              border-bottom: 2px solid #02a6b5;
              border-left: 2px solid #02a6b5;
            }
            &:after {
              position: absolute;
              bottom: 0;
              right: 0;
              content: "";
              width: 10px;
              height: 10px;
              border-bottom: 2px solid #02a6b5;
              border-right: 2px solid #02a6b5;
            }
          }

          h2 {
            height: 0.6rem;
            line-height: 0.6rem;
            text-align: center;
            color: #fff;
            font-size: 0.225rem;
            font-weight: 400;
            a {
              margin: 0 0.1875rem;
              color: #fff;
              text-decoration: none;
            }
          }
          .chart {
            height: 3rem;
          }
        }
      }

    }

  }

}

@-webkit-keyframes rotate {
  from {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  to {
    transform: translate(-50%, -50%) rotate(360deg);
  }
}
@keyframes rotate {
  from {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  to {
    transform: translate(-50%, -50%) rotate(360deg);
  }
}

@-webkit-keyframes rotate1 {
  from {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  to {
    transform: translate(-50%, -50%) rotate(-360deg);
  }
}
@keyframes rotate1 {
  from {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  to {
    transform: translate(-50%, -50%) rotate(-360deg);
  }
}

@media screen and (max-width: 1024px) {
  html {
    font-size: 42px !important;
  }
}
@media screen and (min-width: 1920) {
  html {
    font-size: 80px !important;
  }
}	
</style>
