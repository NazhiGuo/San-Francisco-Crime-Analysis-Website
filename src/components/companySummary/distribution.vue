
<template>
  <div class="distribution-container"> 
    <div class="chart" id="chart_right2"></div>
  </div>
</template>

<script>
export default {
  props:['area'],
  name: "distribution",
  data() {
    return {
      myChart: null,
      chartDataByArea:{
        'BAYVIEW': [
          { name: 'Friday', value: 31225 },
          { name: 'Monday', value: 29100 },
          { name: 'Saturday', value: 28671 },
          { name: 'Sunday', value: 27288 },
          { name: 'Thursday', value: 29195 },
          { name: 'Tuesday', value: 29604 },
          { name: 'Wednesday', value: 30397 }
        ],
        'CENTRAL': [
          { name: 'Friday', value: 34840 },
          { name: 'Monday', value: 29242 },
          { name: 'Saturday', value: 36147 },
          { name: 'Sunday', value: 31498 },
          { name: 'Thursday', value: 30402 },
          { name: 'Tuesday', value: 29330 },
          { name: 'Wednesday', value: 30464 }
        ],
        'INGLESIDE': [
          { name: 'Friday', value: 27285 },
          { name: 'Monday', value: 25896 },
          { name: 'Saturday', value: 25148 },
          { name: 'Sunday', value: 23547 },
          { name: 'Thursday', value: 26132 },
          { name: 'Tuesday', value: 26350 },
          { name: 'Wednesday', value: 26734 }
        ],
        'NA': [
          { name: 'Sunday', value: 1 }
        ],
        'MISSION': [
          { name: 'Friday', value: 43401 },
          { name: 'Monday', value: 39745 },
          { name: 'Saturday', value: 41721 },
          { name: 'Sunday', value: 38763 },
          { name: 'Thursday', value: 41108 },
          { name: 'Tuesday', value: 41383 },
          { name: 'Wednesday', value: 42864 }
        ],
        'NORTHERN': [
          { name: 'Friday', value: 40864 },
          { name: 'Monday', value: 36242 },
          { name: 'Saturday', value: 39613 },
          { name: 'Sunday', value: 36490 },
          { name: 'Thursday', value: 37717 },
          { name: 'Tuesday', value: 37149 },
          { name: 'Wednesday', value: 38360 }
        ],
        'PARK': [
          { name: 'Friday', value: 18424 },
          { name: 'Monday', value: 16931 },
          { name: 'Saturday', value: 16703 },
          { name: 'Sunday', value: 16059 },
          { name: 'Thursday', value: 17106 },
          { name: 'Tuesday', value: 16757 },
          { name: 'Wednesday', value: 17718 }
        ],
        'RICHMOND': [
          { name: 'Friday', value: 17212 },
          { name: 'Monday', value: 15905 },
          { name: 'Saturday', value: 16274 },
          { name: 'Sunday', value: 15290 },
          { name: 'Thursday', value: 16078 },
          { name: 'Tuesday', value: 15799 },
          { name: 'Wednesday', value: 16246 }
        ],
        'SOUTHERN': [
          { name: 'Friday', value: 61192 },
          { name: 'Monday', value: 52474 },
          { name: 'Saturday', value: 58119 },
          { name: 'Sunday', value: 51447 },
          { name: 'Thursday', value: 56267 },
          { name: 'Tuesday', value: 54569 },
          { name: 'Wednesday', value: 56624 }
        ],
        'TARAVAL': [
          { name: 'Friday', value: 23728 },
          { name: 'Monday', value: 22243 },
          { name: 'Saturday', value: 21444 },
          { name: 'Sunday', value: 19954 },
          { name: 'Thursday', value: 22325 },
          { name: 'Tuesday', value: 22742 },
          { name: 'Wednesday', value: 23025 }
        ],
        'TENDERLOIN': [
          { name: 'Friday', value: 25980 },
          { name: 'Monday', value: 26752 },
          { name: 'Saturday', value: 25067 },
          { name: 'Sunday', value: 23651 },
          { name: 'Thursday', value: 27563 },
          { name: 'Tuesday', value: 28772 },
          { name: 'Wednesday', value: 29169 }
        ]
      }
    }
  },
  mounted() {
    this.getEchartRight2();
    this.updateBusinessData(this.area);
  },
  watch: {
    area(newArea) {
      this.updateBusinessData(newArea);
    },
  },
  methods: {
    updateBusinessData(newArea) {
      const data = this.chartDataByArea[newArea];
      if (data) {
        this.getEchartRight2(data);
      } else {
        // 如果没有对应的数据，可以显示默认数据或提示
        console.warn(`未找到区域 ${newArea} 的图表数据`);
        this.getEchartRight2(
            [{
              value: 324151,
              name: 'Friday'
            },{
              value: 294530,
              name: 'Monday'
            },{
              value: 308907,
              name: 'Saturday'
            },{
              value: 283988,
              name: 'Sunday'
            },{
              value: 303893,
              name: 'Thursday'
            },{
              value: 302455,
              name: 'Tuesday'
            },{
              value: 311601,
              name: 'Wednesday'
            }]
        );
      }
    },
    getEchartRight2(data) {
      if (!this.myChart) {
        // 实例化对象
        this.myChart = echarts.init(document.getElementById('chart_right2'));
      }
      else {
        // 清除之前的图表，防止数据重复显示
        this.myChart.clear();
      }
      if (!data) {
        data = [{
          value: 324151,
          name: 'Friday'
        },{
          value: 294530,
          name: 'Monday'
        },{
          value: 308907,
          name: 'Saturday'
        },{
          value: 283988,
          name: 'Sunday'
        },{
          value: 303893,
          name: 'Thursday'
        },{
          value: 302455,
          name: 'Tuesday'
        },{
          value: 311601,
          name: 'Wednesday'
        }];
      }
      let option = {
        color: ['#EAEA26', '#906BF9', '#FE5656', '#01E17E', '#3DD1F9', '#FFAD05', '#4465fc'],
        tooltip: {
          trigger: 'item',
          formatter: '{b} : {c} ({d}%)'
        },
        polar: {},
        angleAxis: {
          interval: 1,
          type: 'category',
          data: [],
          z: 10,
          axisLine: {
            show: false,
            lineStyle: {
              color: '#0B4A6B',
              width: 5,
              type: 'solid'
            },
          },
          axisLabel: {
            interval: 0,
            show: true,
            color: '#0B4A6B',
            margin: 8,
            fontSize: 16
          },
        },
        radiusAxis: {
          min: 40,
          max: 120,
          interval: 20,
          axisLine: {
            show: false,
            lineStyle: {
              color: '#0B3E5E',
              width: 1,
              type: 'solid'
            },
          },
          axisLabel: {
            formatter: '{value} %',
            show: false,
            padding: [0, 0, 20, 0],
            color: '#0B3E5E',
            fontSize: 16
          },
          splitLine: {
            lineStyle: {
              color: '#0B3E5E',
              width: 2,
              type: "solid"
            }
          }
        },
        calculable: true,
        series: [{
          type: 'pie',
          radius: ['6%', '10%'],
          hoverAnimation: false,
          labelLine: {
            normal: {
              show: false,
              length: 30,
              length2: 50
            },
            emphasis: {
              show: false
            }
          },
          tooltip: {
            show: false
          },
          data: [{
            name: '',
            value: 0,
            itemStyle: {
              normal: {
                color: '#0B4A6B'
              }
            }
          }]
        }, {
          type: 'pie',
          radius: ['90%', '95%'],
          hoverAnimation: false,
          labelLine: {
            normal: {
              show: false,
              length: 30,
              length2: 50
            },
            emphasis: {
              show: false
            }
          },
          tooltip: {
            show: false
          },
          data: [{
            name: '',
            value: 0,
            itemStyle: {
              normal: {
                color: '#0B4A6B'
              }
            }
          }]
        },{
          stack: 'a',
          type: 'pie',
          radius: ['20%', '80%'],
          roseType: 'area',
          zlevel: 10,
          label: {
            normal: {
              show: true,
              formatter: '{b}',
              textStyle: {
                fontSize: 12,
              },
              position: 'outside'
            },
            emphasis: {
              show: false
            }
          },
          labelLine: {
            normal: {
              show: true,
              length: 15,
              length2: 50,
              lineStyle: {
                type: 'dotted' 
              } 
            },
            emphasis: {
              show: true
            }
          },
          data: data
        }]
      }

      this.myChart.setOption(option, true);
      window.addEventListener('resize', () => {
        this.myChart.resize();
      });
    },
  },
  beforeDestroy() {
    
  }
};
</script>

<style lang="scss" scoped>
.distribution-container {
  .chart {
    height: 3rem;
  }
}
</style>
