
<template>
  <div class="business-container"> 
    <div class="chart" id="chart_left1"></div>   
  </div>
</template>

<script>
export default {
  props: ['area'],
  name: "business",
  data() {
    return {
      myChart: null, // 存储图表实例
      chartDataByArea: {
        'BAYVIEW': {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [13275, 13562, 13890, 13055, 13915, 13415, 12687],
        },
        'CENTRAL': {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [18638, 17367, 18210, 17036, 14542, 13727, 12463],
        },
        'INGLESIDE': {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [10842, 10919, 12592, 12000, 12403, 11682, 11057],
        },
        'MISSION': {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [21211, 19064, 17951, 18622, 20415, 18085, 17525],
        },
        'NORTHERN': {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [20687, 19768, 19721, 18056, 17762, 15996, 14269],
        },
        'PARK': {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [8246, 8355, 9021, 9033, 9140, 8426, 7145],
        },
        'RICHMOND': {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [9217, 8710, 8810, 7730, 8210, 7415, 6335],
        },
        'SOUTHERN': {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [27800, 27859, 29441, 28224, 28618, 25270, 23955],
        },
        'TARAVAL': {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [11073, 10710, 11392, 9931, 10060, 9975, 9248],
        },
        'TENDERLOIN': {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [8498, 9679, 10431, 11157, 12599, 11473, 12029],
        },
        // 添加更多区域的数据...
      },
    }
  },
  mounted() {
    this.getEchartLeft1();
  },
  watch: {
    area(newArea) {
      this.updateBusinessData(newArea);
    },
  },
  methods: {
    updateBusinessData(newArea) {
      const chartData = this.chartDataByArea[newArea];
      if (chartData) {
        this.getEchartLeft1(chartData);
      } else {
        // 如果没有对应的数据，可以显示默认数据或提示
        console.warn(`未找到区域 ${newArea} 的图表数据`);
        this.getEchartLeft1({
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [149487, 145994, 151459, 144844, 147664, 135464, 126713]
        });
      }
    },
    getEchartLeft1(charts) {
      // 实例化对象
      if (!this.myChart) {
        // 实例化对象
        this.myChart = echarts.init(document.getElementById('chart_left1'));
      }

      if (!charts) {
        charts = {
          cityList: ['2017', '2016', '2015', '2014', '2013', '2012', '2011'],
          cityData: [149487, 145994, 151459, 144844, 147664, 135464, 126713]
        };
      }

      let top10CityList = charts.cityList;
      let top10CityData = charts.cityData;
      let color = ['rgba(14,109,236', 'rgba(255,91,6', 'rgba(100,255,249', 'rgba(248,195,248', 'rgba(110,234,19', 'rgba(255,168,17', 'rgba(218,111,227'];

      let lineY = [];
      for (let i = 0; i < charts.cityList.length; i++) {
        let x = i
        if (x > color.length - 1) {
          x = color.length - 1
        }
        let data = {
          name: charts.cityList[i],
          color: color[x] + ')',
          value: top10CityData[i],
          itemStyle: {
            normal: {
              show: true,
              color: new echarts.graphic.LinearGradient(0, 0, 1, 0, [{
                offset: 0,
                color: color[x] + ', 0.3)'
              }, {
                offset: 1,
                color: color[x] + ', 1)'
              }], false),
              barBorderRadius: 10
            },
            emphasis: {
              shadowBlur: 15,
              shadowColor: 'rgba(0, 0, 0, 0.1)'
            }
          }
        }
        lineY.push(data)
      }  

      // 指定配置和数据
      let option = {
        color: color,
        tooltip: {
          trigger: 'item',
        },
        grid: {
          borderWidth: 0,
          top: '5%',
          left: '2%',
          right: '2%',
          bottom: '0%',
          containLabel: true
        },
        xAxis: [{
          type: 'value',
          axisTick: {
            show: false
          },
          axisLine: {
            show: false
          },
          splitLine: {
            show: false
          },
          axisLabel: {
            show: false
          }
        }],
        yAxis: [{
          type: 'category',
          inverse: true,
          axisTick: {
            show: false
          },
          axisLine: {
            show: false
          },
          axisLabel: {
            show: true,
            inside: false,
            textStyle: {
              color: '#b3ccf8',
              fontSize: 13
            },
          },
          data: top10CityList
        }, {
          type: 'category',
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            show: true,
            inside: false,
            textStyle: {
              color: '#b3ccf8',
              fontSize: 13
            },
            formatter: (val) => {
              return `${val}`
            }
          },
          splitArea: {
            show: false
          },
          splitLine: {
            show: false
          },
          data: top10CityData.reverse()
        }],
        series: [{
          name: '',
          type: 'bar',
          zlevel: 2,
          barWidth: '10px',
          data: lineY,
          animationDuration: 1500,
          label: {
            normal: {
              color: '#b3ccf8',
              show: false,
              position: [0, '-15px'],
              textStyle: {
                fontSize: 13
              },
              formatter: (a, b) => {
                return a.name;
              }
            }
          }
        }]
      };

      // 把配置给实例对象
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
.business-container {
  .chart {
    height: 3rem;
  }
}
</style>
