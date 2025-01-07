
<template>
  <div class="talent-container"> 
    <div class="chart" id="chart_left2"></div>   
  </div>
</template>

<script>
export default {
  props:['area'],
  name: "talent",
  data() {
    return {
      myChart: null, // 存储图表实例
      chartDataByArea: {
        'BAYVIEW': [
          { name: 'Property Crime', value: 73063 },
          { name: 'Non-Criminal', value: 46650 },
          { name: 'Other', value: 39721 },
          { name: 'Violent Crime', value: 28410 },
          { name: 'Drug', value: 10879 },
          { name: 'Public Order Crime', value: 2678 },
          { name: 'Weapon Related Crime', value: 4079 }
        ],
        'CENTRAL': [
          { name: 'Property Crime', value: 115982 },
          { name: 'Non-Criminal', value: 48492 },
          { name: 'Other', value: 22243 },
          { name: 'Violent Crime', value: 22467 },
          { name: 'Drug', value: 5771 },
          { name: 'Public Order Crime', value: 5712 },
          { name: 'Weapon Related Crime', value: 1256 }
        ],
        'INGLESIDE': [
          { name: 'Property Crime', value: 73438 },
          { name: 'Non-Criminal', value: 40704 },
          { name: 'Other', value: 31445 },
          { name: 'Violent Crime', value: 25010 },
          { name: 'Drug', value: 6122 },
          { name: 'Public Order Crime', value: 1744 },
          { name: 'Weapon Related Crime', value: 2629 }
        ],
        'MISSION': [
          { name: 'Property Crime', value: 99071 },
          { name: 'Non-Criminal', value: 67648 },
          { name: 'Other', value: 46378 },
          { name: 'Violent Crime', value: 36557 },
          { name: 'Drug', value: 22487 },
          { name: 'Public Order Crime', value: 13516 },
          { name: 'Weapon Related Crime', value: 3328 }
        ],
        'NA': [
          { name: 'Property Crime', value: 1 }
        ],
        'NORTHERN': [
          { name: 'Property Crime', value: 134781 },
          { name: 'Non-Criminal', value: 52770 },
          { name: 'Other', value: 30312 },
          { name: 'Violent Crime', value: 26648 },
          { name: 'Drug', value: 12200 },
          { name: 'Public Order Crime', value: 7791 },
          { name: 'Weapon Related Crime', value: 1933 }
        ],
        'PARK': [
          { name: 'Property Crime', value: 52417 },
          { name: 'Non-Criminal', value: 31910 },
          { name: 'Other', value: 15537 },
          { name: 'Violent Crime', value: 10309 },
          { name: 'Drug', value: 7145 },
          { name: 'Public Order Crime', value: 1521 },
          { name: 'Weapon Related Crime', value: 859 }
        ],
        'RICHMOND': [
          { name: 'Property Crime', value: 57798 },
          { name: 'Non-Criminal', value: 26681 },
          { name: 'Other', value: 13968 },
          { name: 'Violent Crime', value: 9260 },
          { name: 'Drug', value: 3360 },
          { name: 'Public Order Crime', value: 1046 },
          { name: 'Weapon Related Crime', value: 691 }
        ],
        'SOUTHERN': [
          { name: 'Property Crime', value: 170776 },
          { name: 'Non-Criminal', value: 94608 },
          { name: 'Other', value: 50484 },
          { name: 'Violent Crime', value: 40757 },
          { name: 'Drug', value: 24191 },
          { name: 'Public Order Crime', value: 6949 },
          { name: 'Weapon Related Crime', value: 2927 }
        ],
        'TARAVAL': [
          { name: 'Property Crime', value: 73052 },
          { name: 'Non-Criminal', value: 37369 },
          { name: 'Other', value: 21726 },
          { name: 'Violent Crime', value: 15399 },
          { name: 'Drug', value: 4505 },
          { name: 'Public Order Crime', value: 2138 },
          { name: 'Weapon Related Crime', value: 1272 }
        ],
        'TENDERLOIN': [
          { name: 'Property Crime', value: 39310 },
          { name: 'Non-Criminal', value: 45629 },
          { name: 'Other', value: 30074 },
          { name: 'Violent Crime', value: 23596 },
          { name: 'Drug', value: 39413 },
          { name: 'Public Order Crime', value: 6902 },
          { name: 'Weapon Related Crime', value: 2030 }
        ]
      }
    }
  },
  mounted() {
    this.getEchartLeft2();
  },
  watch: {
    area(newArea) {
      this.updateBusinessData(newArea);
    },
  },
  methods: {
    updateBusinessData(newArea) {
      const scaleData = this.chartDataByArea[newArea];
      if (scaleData) {
        this.getEchartLeft2(scaleData);
      } else {
        // 如果没有对应的数据，可以显示默认数据或提示
        console.warn(`未找到区域 ${newArea} 的图表数据`);
        this.getEchartLeft2(
            [{
              name: 'Property Crime',
              value: 889689
            },{
              name: 'Non-Criminal',
              value: 492461
            },{
              name: 'Other',
              value: 301888
            },{
              name: 'Violent Crime',
              value: 238413
            },{
              name: 'Drug',
              value: 136073
            },{
              name: 'Public Order Crime',
              value: 49997
            },{
              name: 'Weapon Related Crime',
              value: 21004
            }]
        );
      }
    },
    getEchartLeft2(scaleData) {
      if (!this.myChart) {
        // 实例化对象
        this.myChart = echarts.init(document.getElementById('chart_left2'));
      }
      if (!scaleData) {
        scaleData = [{
          name: 'Property Crime',
          value: 889689
        },{
          name: 'Non-Criminal',
          value: 492461
        },{
          name: 'Other',
          value: 301888
        },{
          name: 'Violent Crime',
          value: 238413
        },{
          name: 'Drug',
          value: 136073
        },{
          name: 'Public Order Crime',
          value: 49997
        },{
          name: 'Weapon Related Crime',
          value: 21004
        }];
      }
      let rich = {
        white: {
          color: '#ddd',
          align: 'center',
          padding: [3, 0]
        }
      };
      let placeHolderStyle = {
        normal: {
          label: {
            show: false
          },
          labelLine: {
            show: false
          },
          color: 'rgba(0, 0, 0, 0)',
          borderColor: 'rgba(0, 0, 0, 0)',
          borderWidth: 0
        }
      };
      let data = [];
      let color=['#00ffff', '#007fff', '#00ff00', '#ffea00', '#ff7f00', '#ff0000', '#8000ff']
      for (let i = 0; i < scaleData.length; i++) {
        data.push({
          value: scaleData[i].value,
          name: scaleData[i].name,
          itemStyle: {
            normal: {
              borderWidth: 6,
              shadowBlur: 10,
              borderColor: color[i],
              shadowColor: color[i]
            }
          }
        }, {
          value: 2,
          name: '',
          itemStyle: placeHolderStyle
        });
      }

      let option = {
        series: [{
          name: '',
          type: 'pie',
          clockWise: false,
          radius: ['66%', '68%'],
          center: ['50%', '50%'],
          hoverAnimation: false,
          itemStyle: {
            normal: {
              label: {
                show: true,
                position: 'outside',
                color: '#ddd',
                formatter: (params) => {
                  let percent = 0;
                  let total = 0;
                  for (let i = 0; i < scaleData.length; i++) {
                    total += scaleData[i].value;
                  }
                  percent = ((params.value / total) * 100).toFixed(0);
                  if (params.name !== '') {
                    return params.name + '\n{white|' + '占比' + percent + '%}';
                  } else {
                    return '';
                  }
                },
                rich: rich
              },
              labelLine: {
                length: 10,
                length2: 30,
                show: true,
                color: '#00ffff'
              }
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
.talent-container {
  .chart {
    height: 3rem;
  }
}
</style>
