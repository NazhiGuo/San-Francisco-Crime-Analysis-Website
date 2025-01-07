
<!--<template>-->
<!--  <div class="word-container">-->
<!--    <div class="chart" id="chart_right1"></div>-->
<!--  </div>-->
<!--</template>-->

<!--<script>-->
<!--import '@/assets/js/echarts-wordcloud.min'-->

<!--export default {-->
<!--  name: "wordCloud",-->
<!--  data() {-->
<!--    return {-->
<!--      timer: null-->
<!--    }-->
<!--  },-->
<!--  mounted() {-->
<!--    this.getEchartRight1();-->
<!--    this.timer = setInterval(() => {-->
<!--      this.getEchartRight1();-->
<!--    }, 5000)-->
<!--  },-->
<!--  methods: {-->
<!--    getEchartRight1() {-->
<!--      let myChart = echarts.init(document.getElementById('chart_right1'));-->
<!--      let option = {-->
<!--        // tooltip: {-->
<!--        //   show: false-->
<!--        // },-->
<!--        series: [{-->
<!--          type: 'wordCloud',-->
<!--          gridSize: 1,-->
<!--          sizeRange: [12, 50],-->
<!--          rotationRange: [-90, 90],-->
<!--          rotationStep: 45,-->
<!--          shape: 'diamond',-->
<!--          width: '90%',-->
<!--          textPadding: 0,-->
<!--          autoSize: {-->
<!--            enable: true,-->
<!--            minSize: 6-->
<!--          },-->
<!--          textStyle: {-->
<!--            normal: {-->
<!--              textBorderColor: 'rgba(255,255,255,0.3)',-->
<!--              textBorderWidth: 1,-->
<!--              color: () => {-->
<!--                return 'rgb(' + [-->
<!--                  Math.round(Math.random() * 160),-->
<!--                  Math.round(Math.random() * 160),-->
<!--                  Math.round(Math.random() * 160)-->
<!--                ].join(',') + ')';-->
<!--              }-->
<!--            },-->
<!--            emphasis: {-->
<!--              fontSize: 20,-->
<!--              // shadowBlur: 10,-->
<!--              // shadowColor: 'rgba(255,255,255, .1)'-->
<!--            }-->
<!--          },-->
<!--          data: [{-->
<!--            name: '区块链',-->
<!--            value: 810-->
<!--          }, {-->
<!--            name: '云计算',-->
<!--            value: 520-->
<!--          },{-->
<!--            name: "人工智能",-->
<!--            value: 928-->
<!--          },{-->
<!--            name: "大数据",-->
<!--            value: 906-->
<!--          },{-->
<!--            name: "工业互联网",-->
<!--            value: 825-->
<!--          },{-->
<!--            name: "医疗",-->
<!--            value: 514-->
<!--          },{-->
<!--            name: "质量溯源",-->
<!--            value: 486-->
<!--          },{-->
<!--            name: "政务",-->
<!--            value: 53-->
<!--          },{-->
<!--            name: "密码学",-->
<!--            value: 927-->
<!--          },{-->
<!--            name: "金融行业",-->
<!--            value: 1308-->
<!--          },{-->
<!--            name: "供应链",-->
<!--            value: 693-->
<!--          },{-->
<!--            name: "公有链",-->
<!--            value: 611-->
<!--          },{-->
<!--            name: "私有链",-->
<!--            value: 512-->
<!--          },{-->
<!--            name: "联盟链",-->
<!--            value: 382-->
<!--          },{-->
<!--            name: "数据共享",-->
<!--            value: 312-->
<!--          },{-->
<!--            name: "文创版权",-->
<!--            value: 187-->
<!--          },{-->
<!--            name: "天河链",-->
<!--            value: 163-->
<!--          },{-->
<!--            name: "数据存证",-->
<!--            value: 104-->
<!--          },{-->
<!--            name: "UDFS存储",-->
<!--            value: 3-->
<!--          },{-->
<!--            name: "在线教育",-->
<!--            value: 31-->
<!--          },{-->
<!--            name: "关联分析",-->
<!--            value: 941-->
<!--          },{-->
<!--            name: "智慧停车",-->
<!--            value: 585-->
<!--          },{-->
<!--            name: "链云生态",-->
<!--            value: 473-->
<!--          },{-->
<!--            name: "应用层",-->
<!--            value: 358-->
<!--          },{-->
<!--            name: "网络层",-->
<!--            value: 246-->
<!--          },{-->
<!--            name: "数据层",-->
<!--            value: 207-->
<!--          },{-->
<!--            name: "基础层",-->
<!--            value: 194-->
<!--          },{-->
<!--            name: "智能合约",-->
<!--            value: 104-->
<!--          },{-->
<!--            name: "去中心化",-->
<!--            value: 87-->
<!--          },{-->
<!--            name: "数字货币",-->
<!--            value: 415-->
<!--          },{-->
<!--            name: "酷屏",-->
<!--            value: 253-->
<!--          },{-->
<!--            name: "可视化",-->
<!--            value: 211-->
<!--          },{-->
<!--            name: "P2P",-->
<!--            value: 116-->
<!--          },{-->
<!--            name: "数据挖掘",-->
<!--            value: 1309-->
<!--          }]-->
<!--        }]-->
<!--      }-->

<!--      myChart.setOption(option, true);-->
<!--      window.addEventListener('resize', () => {-->
<!--        myChart.resize();-->
<!--      });-->
<!--    },-->
<!--  },-->
<!--  beforeDestroy() {-->
<!--    clearInterval(this.timer);-->
<!--  }-->
<!--};-->
<!--</script>-->

<!--<style lang="scss" scoped>-->
<!--.word-container {-->
<!--  .chart {-->
<!--    height: 3rem;-->
<!--  }-->
<!--}-->
<!--</style>-->
<template>
  <div class="word-container">
    <div class="chart" id="chart_right1"></div>
  </div>
</template>

<script>
// import '@/assets/js/echarts-wordcloud.min'
export default {
  props:['area'],
  name: "wordCloud",
  data() {
    return {
      myChart: null,
      data:{
        'MISSION': 0.43360728065470525,
        'BAYVIEW': 0.37627019661280904,
        'CENTRAL': 0.26419523888916423,
        'TARAVAL': 0.26868475051620667,
        'TENDERLOIN': 0.626250307562288,
        'INGLESIDE': 0.3151602500386544,
        'PARK': 0.33053183846012466,
        'SOUTHERN': 0.36718182097406654,
        'RICHMOND': 0.24101095705826033,
        'NORTHERN': 0.2979525963180513,
        'ALL':0.3600648031838086
      },
      timer: null
    };
  },
  mounted() {
    this.getEchartRight1();
  },
  watch: {
    area(newArea) {
      this.updateBusinessData(newArea);
    },
  },
  methods: {
    updateBusinessData(newArea) {
      const ps = this.data[newArea];
      if (ps) {
        this.getEchartRight1([ps]);
      } else {
        // 如果没有对应的数据，可以显示默认数据或提示
        console.warn(`未找到区域 ${newArea} 的图表数据`);
        this.getEchartRight1([0.36])
      }
    },
    getEchartRight1(ps) {
      if (!this.myChart) {
        // 实例化对象
        this.myChart = echarts.init(document.getElementById('chart_right1'));
      }
      if(!ps){
        ps=[0.36]
      }
      // let myChart = echarts.init(document.getElementById('chart_right1'));
      let option = {
        series: [
          {
            type: 'liquidFill',
            data: ps,  // 水球填充的数值，表示 45%
            radius: '70%',
            color: ['#00b9f5'],  // 水球的颜色
            backgroundStyle: {
              color: 'rgba(0, 0, 0, 0.5)',  // 背景颜色
              borderColor: '#007bff',
              borderWidth: 3,
              shadowColor: 'rgba(0, 123, 225, 0.4)',
              shadowBlur: 20
            },
            outline: {
              show: false,  // 是否显示外边框
            }
          }
        ]
      };

      this.myChart.setOption(option, true);
      window.addEventListener('resize', () => {
        this.myChart.resize();
      });
    }
  },
  beforeDestroy() {
    clearInterval(this.timer);
  }
};
</script>

<style lang="scss" scoped>
.word-container {
  position: relative;
  width: 100%; // 设定宽度为父级的 100%
  height: 100%; // 确定容器高度
  margin-top: -30px;
  //margin-top: -60px;
  //padding-top: 0;
  //margin-left: 30px;
  //width: 432px;
  //height: 400px;
  .chart {
    height: 100%;
    width: 100%;
  }
}
</style>
