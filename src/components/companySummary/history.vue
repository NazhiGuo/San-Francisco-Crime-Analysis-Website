

<!--&lt;!&ndash;<template>&ndash;&gt;-->
<!--&lt;!&ndash;  <div class="history-container">&ndash;&gt;-->
<!--&lt;!&ndash;    <div class="tabs">&ndash;&gt;-->
<!--&lt;!&ndash;      <ul class="tab-tilte">&ndash;&gt;-->
<!--&lt;!&ndash;        <li v-for="(itemTit, index) in tabTitle" :key="index" @mouseover="handleMouseOver(index)"&ndash;&gt;-->
<!--&lt;!&ndash;          @mouseout="handleMouseOut(index)" :class="{ active: cur == index }">&ndash;&gt;-->
<!--&lt;!&ndash;          {{ itemTit }}&ndash;&gt;-->
<!--&lt;!&ndash;        </li>&ndash;&gt;-->
<!--&lt;!&ndash;      </ul>&ndash;&gt;-->
<!--&lt;!&ndash;      <div class="indicatorDots">&ndash;&gt;-->
<!--&lt;!&ndash;        <span :class="{ active: cur == i }" v-for="(v, i) in tabTitle" :key="i"></span>&ndash;&gt;-->
<!--&lt;!&ndash;      </div>&ndash;&gt;-->
<!--&lt;!&ndash;      <div class="tab-content">&ndash;&gt;-->
<!--&lt;!&ndash;        <div v-for="(itemCon, index) in tabCon" v-show="cur == index" :key="index">&ndash;&gt;-->
<!--&lt;!&ndash;          <div v-for="(v, i) in itemCon" :key="i" class="content">&ndash;&gt;-->
<!--&lt;!&ndash;            {{ v }}&ndash;&gt;-->
<!--&lt;!&ndash;          </div>&ndash;&gt;-->
<!--&lt;!&ndash;        </div>&ndash;&gt;-->
<!--&lt;!&ndash;      </div>&ndash;&gt;-->
<!--&lt;!&ndash;    </div>&ndash;&gt;-->
<!--&lt;!&ndash;  </div>&ndash;&gt;-->
<!--&lt;!&ndash;</template>&ndash;&gt;-->

<!--&lt;!&ndash;<script>&ndash;&gt;-->
<!--&lt;!&ndash;export default {&ndash;&gt;-->
<!--&lt;!&ndash;  name: "history",&ndash;&gt;-->
<!--&lt;!&ndash;  data() {&ndash;&gt;-->
<!--&lt;!&ndash;    return {&ndash;&gt;-->
<!--&lt;!&ndash;      timer: null,&ndash;&gt;-->
<!--&lt;!&ndash;      tabTitle: ['2012', '2013', '2014', '2015', '2016', '2017'],&ndash;&gt;-->
<!--&lt;!&ndash;      tabCon: [&ndash;&gt;-->
<!--&lt;!&ndash;        [&ndash;&gt;-->
<!--&lt;!&ndash;          '2015.10，公司成立，正式布局区块链、大数据方向',&ndash;&gt;-->
<!--&lt;!&ndash;          '2015.11，与国家超算吕梁云计算中心签订战略合作协议',&ndash;&gt;-->
<!--&lt;!&ndash;          '2015.12，建设高性能计算服务平台，基于区块链技术打造文创基础云平台'&ndash;&gt;-->
<!--&lt;!&ndash;        ],&ndash;&gt;-->
<!--&lt;!&ndash;        [&ndash;&gt;-->
<!--&lt;!&ndash;          '2016.03，公司提供的高性能计算服务得到中科院认可，就此达成合作',&ndash;&gt;-->
<!--&lt;!&ndash;          '2016.07，与国家超算广州中心签订战略合作协议，启动区块链底层公链开发技术论证',&ndash;&gt;-->
<!--&lt;!&ndash;          '2016.10，启动区块链底层公链开发，开拓数字资产管理业务',&ndash;&gt;-->
<!--&lt;!&ndash;          '2016.11，与国家超级计算长沙中心签订战略合作协议'&ndash;&gt;-->
<!--&lt;!&ndash;        ],&ndash;&gt;-->
<!--&lt;!&ndash;        [&ndash;&gt;-->
<!--&lt;!&ndash;          '2017.03，与国家级长沙经开区共建博士创新创业园',&ndash;&gt;-->
<!--&lt;!&ndash;          '2017.07，开发GBI区块链资讯信息平台',&ndash;&gt;-->
<!--&lt;!&ndash;          '2017.09，打造区块链信息服务平台，开拓区块链安全业务',&ndash;&gt;-->
<!--&lt;!&ndash;          '2017.12，区块链底层公链测试链上线运行，启动链上DAPP开发'&ndash;&gt;-->
<!--&lt;!&ndash;        ],&ndash;&gt;-->
<!--&lt;!&ndash;        [&ndash;&gt;-->
<!--&lt;!&ndash;          '2018.05，与长沙经开区共建区块链产业园，区块链底层公链上线运行',&ndash;&gt;-->
<!--&lt;!&ndash;          '2018.08，公链分布式存储网络正式运行',&ndash;&gt;-->
<!--&lt;!&ndash;          '2018.10，区块链安全技术检测中心正式运行，公链多侧链技术落地，链上应用上线',&ndash;&gt;-->
<!--&lt;!&ndash;          '2018.12，被评为中国区块链百强企业'&ndash;&gt;-->
<!--&lt;!&ndash;        ],&ndash;&gt;-->
<!--&lt;!&ndash;        [&ndash;&gt;-->
<!--&lt;!&ndash;          '2019.03，上线分布式存储系统UDFS，更新优壹号V2.0.0版，完成Ulord V2.0版白皮书全部规划',&ndash;&gt;-->
<!--&lt;!&ndash;          '2019.07，文创版权公共服务平台优版权正式上线',&ndash;&gt;-->
<!--&lt;!&ndash;          '2019.08，承担国家网信办区块链相关课题研究',&ndash;&gt;-->
<!--&lt;!&ndash;        ],&ndash;&gt;-->
<!--&lt;!&ndash;        [&ndash;&gt;-->
<!--&lt;!&ndash;          '2020.03，完成分布式计算框架和贡献证明算法的设计和开发',&ndash;&gt;-->
<!--&lt;!&ndash;          '2020.05，完成分布式计算资源动态调度和管理开发',&ndash;&gt;-->
<!--&lt;!&ndash;          '2020.10，推出链云计算生态，完成计算平台和API接口开发，完成优壹号对计算Dapp支持'&ndash;&gt;-->
<!--&lt;!&ndash;        ]&ndash;&gt;-->
<!--&lt;!&ndash;      ],&ndash;&gt;-->
<!--&lt;!&ndash;      cur: 0, //默认选中第一个tab&ndash;&gt;-->
<!--&lt;!&ndash;    }&ndash;&gt;-->
<!--&lt;!&ndash;  },&ndash;&gt;-->
<!--&lt;!&ndash;  mounted() {&ndash;&gt;-->
<!--&lt;!&ndash;    this.getTimer();&ndash;&gt;-->
<!--&lt;!&ndash;  },&ndash;&gt;-->
<!--&lt;!&ndash;  methods: {&ndash;&gt;-->
<!--&lt;!&ndash;    getTimer() {&ndash;&gt;-->
<!--&lt;!&ndash;      this.timer = setInterval(() => {&ndash;&gt;-->
<!--&lt;!&ndash;        this.cur++;&ndash;&gt;-->
<!--&lt;!&ndash;        if (this.cur == this.tabTitle.length) {&ndash;&gt;-->
<!--&lt;!&ndash;          this.cur = 0;&ndash;&gt;-->
<!--&lt;!&ndash;        }&ndash;&gt;-->
<!--&lt;!&ndash;      }, 2000)&ndash;&gt;-->
<!--&lt;!&ndash;    },&ndash;&gt;-->
<!--&lt;!&ndash;    handleMouseOver(index) {&ndash;&gt;-->
<!--&lt;!&ndash;      this.cur = index;&ndash;&gt;-->
<!--&lt;!&ndash;      clearInterval(this.timer);&ndash;&gt;-->
<!--&lt;!&ndash;    },&ndash;&gt;-->
<!--&lt;!&ndash;    handleMouseOut() {&ndash;&gt;-->
<!--&lt;!&ndash;      this.getTimer();&ndash;&gt;-->
<!--&lt;!&ndash;    }&ndash;&gt;-->
<!--&lt;!&ndash;  },&ndash;&gt;-->
<!--&lt;!&ndash;  beforeDestroy() {&ndash;&gt;-->
<!--&lt;!&ndash;    clearInterval(this.timer);&ndash;&gt;-->
<!--&lt;!&ndash;  }&ndash;&gt;-->
<!--&lt;!&ndash;};&ndash;&gt;-->
<!--&lt;!&ndash;</script>&ndash;&gt;-->

<!--&lt;!&ndash;<style lang="scss" scoped>&ndash;&gt;-->
<!--&lt;!&ndash;.history-container {&ndash;&gt;-->
<!--&lt;!&ndash;  margin: 0 0.125rem;&ndash;&gt;-->

<!--&lt;!&ndash;  .tabs {&ndash;&gt;-->
<!--&lt;!&ndash;    display: flex;&ndash;&gt;-->

<!--&lt;!&ndash;    .tab-tilte {&ndash;&gt;-->
<!--&lt;!&ndash;      li {&ndash;&gt;-->
<!--&lt;!&ndash;        color: #fff;&ndash;&gt;-->
<!--&lt;!&ndash;        background-color: rgba(36, 196, 255, 0.5);&ndash;&gt;-->
<!--&lt;!&ndash;        text-align: center;&ndash;&gt;-->
<!--&lt;!&ndash;        cursor: pointer;&ndash;&gt;-->
<!--&lt;!&ndash;        font-size: 0.125rem;&ndash;&gt;-->
<!--&lt;!&ndash;        width: 1.0rem;&ndash;&gt;-->
<!--&lt;!&ndash;        height: 0.35rem;&ndash;&gt;-->
<!--&lt;!&ndash;        line-height: 0.35rem;&ndash;&gt;-->
<!--&lt;!&ndash;        margin-bottom: 0.175rem;&ndash;&gt;-->
<!--&lt;!&ndash;        -webkit-border-radius: 5px;&ndash;&gt;-->
<!--&lt;!&ndash;        -ms-border-radius: 5px;&ndash;&gt;-->
<!--&lt;!&ndash;        -o-border-radius: 5px;&ndash;&gt;-->
<!--&lt;!&ndash;        -moz-border-radius: 5px;&ndash;&gt;-->
<!--&lt;!&ndash;        border-radius: 5px;&ndash;&gt;-->

<!--&lt;!&ndash;        &.active {&ndash;&gt;-->
<!--&lt;!&ndash;          background: linear-gradient(to right, #1b81bc, 20%, #24c4ff);&ndash;&gt;-->
<!--&lt;!&ndash;          color: #fff;&ndash;&gt;-->
<!--&lt;!&ndash;        }&ndash;&gt;-->
<!--&lt;!&ndash;      }&ndash;&gt;-->
<!--&lt;!&ndash;    }&ndash;&gt;-->

<!--&lt;!&ndash;    .indicatorDots {&ndash;&gt;-->
<!--&lt;!&ndash;      background-color: rgba(36, 196, 255, 0.5);&ndash;&gt;-->
<!--&lt;!&ndash;      width: 1px;&ndash;&gt;-->
<!--&lt;!&ndash;      height: 2.8rem;&ndash;&gt;-->
<!--&lt;!&ndash;      margin: 0.0625rem 0 0 0.375rem;&ndash;&gt;-->

<!--&lt;!&ndash;      span {&ndash;&gt;-->
<!--&lt;!&ndash;        display: block;&ndash;&gt;-->
<!--&lt;!&ndash;        height: 0.525rem;&ndash;&gt;-->
<!--&lt;!&ndash;        margin-left: -0.0875rem;&ndash;&gt;-->

<!--&lt;!&ndash;        &:after {&ndash;&gt;-->
<!--&lt;!&ndash;          content: '';&ndash;&gt;-->
<!--&lt;!&ndash;          display: block;&ndash;&gt;-->
<!--&lt;!&ndash;          width: 0.125rem;&ndash;&gt;-->
<!--&lt;!&ndash;          height: 0.125rem;&ndash;&gt;-->
<!--&lt;!&ndash;          background: #ddd;&ndash;&gt;-->
<!--&lt;!&ndash;          -webkit-border-radius: 50%;&ndash;&gt;-->
<!--&lt;!&ndash;          -ms-border-radius: 50%;&ndash;&gt;-->
<!--&lt;!&ndash;          -o-border-radius: 50%;&ndash;&gt;-->
<!--&lt;!&ndash;          -moz-border-radius: 50%;&ndash;&gt;-->
<!--&lt;!&ndash;          border-radius: 50%;&ndash;&gt;-->
<!--&lt;!&ndash;          border: 2px solid #1b81bc;&ndash;&gt;-->
<!--&lt;!&ndash;        }&ndash;&gt;-->

<!--&lt;!&ndash;        &.active {&ndash;&gt;-->
<!--&lt;!&ndash;          &:after {&ndash;&gt;-->
<!--&lt;!&ndash;            background: #24c4ff;&ndash;&gt;-->
<!--&lt;!&ndash;            -webkit-box-shadow: 0 0 0.125rem #1b81bc;&ndash;&gt;-->
<!--&lt;!&ndash;            box-shadow: 0 0 0.125rem #1b81bc;&ndash;&gt;-->
<!--&lt;!&ndash;          }&ndash;&gt;-->
<!--&lt;!&ndash;        }&ndash;&gt;-->
<!--&lt;!&ndash;      }&ndash;&gt;-->
<!--&lt;!&ndash;    }&ndash;&gt;-->

<!--&lt;!&ndash;    .tab-content {&ndash;&gt;-->
<!--&lt;!&ndash;      display: flex;&ndash;&gt;-->
<!--&lt;!&ndash;      align-items: center;&ndash;&gt;-->

<!--&lt;!&ndash;      div {&ndash;&gt;-->
<!--&lt;!&ndash;        margin-left: 0.1875rem;&ndash;&gt;-->
<!--&lt;!&ndash;        color: #fff;&ndash;&gt;-->

<!--&lt;!&ndash;        .content {&ndash;&gt;-->
<!--&lt;!&ndash;          font-size: 0.175rem;&ndash;&gt;-->
<!--&lt;!&ndash;          line-height: 0.275rem;&ndash;&gt;-->
<!--&lt;!&ndash;          padding: 0.1rem 0;&ndash;&gt;-->
<!--&lt;!&ndash;        }&ndash;&gt;-->
<!--&lt;!&ndash;      }&ndash;&gt;-->
<!--&lt;!&ndash;    }&ndash;&gt;-->
<!--&lt;!&ndash;  }&ndash;&gt;-->
<!--&lt;!&ndash;}&ndash;&gt;-->
<!--&lt;!&ndash;</style>&ndash;&gt;-->
<!--<template>-->
<!--  <div class="history-container">-->
<!--    <div class="wrap-container sn-container">-->
<!--      <div class="sn-content">-->
<!--        <div class="sn-title"></div>-->
<!--        <div class="sn-body">-->
<!--          <div class="wrap-container">-->
<!--            <div class="chartsdom" id="chart_arc"></div>-->
<!--          </div>-->
<!--        </div>-->
<!--      </div>-->
<!--    </div>-->
<!--  </div>-->
<!--</template>-->

<!--<script>-->
<!--import * as echarts from 'echarts';-->
<!--const ALL_AREA_DATA = {-->
<!--  'BAYVIEW': [18645, 16697, 18338, 17159, 17426, 16293, 17015, 17484, 16844, 17728, 16243, 15608],-->
<!--  'CENTRAL': [19414, 17380, 19288, 19000, 18189, 17741, 19504, 18994, 18293, 19246, 17181, 17693],-->
<!--  'INGLESIDE': [16200, 15281, 16628, 15718, 15155, 13886, 14612, 14736, 14911, 15672, 14139, 14154],-->
<!--  'MISSION': [26172, 23413, 25678, 24749, 24464, 22687, 23375, 24345, 23919, 25023, 23345, 21815],-->
<!--  'NORTHERN': [24205, 21491, 23696, 22699, 22196, 20786, 22222, 22497, 21169, 22698, 21429, 21347],-->
<!--  'PARK': [10561, 9385, 10619, 10802, 10209, 9429, 9658, 10257, 9967, 10370, 9606, 8835],-->
<!--  'RICHMOND': [9867, 9144, 10093, 9902, 9873, 8927, 9033, 9523, 9239, 9695, 8652, 8856],-->
<!--  'SOUTHERN': [33803, 30539, 34106, 32855, 32936, 31873, 32838, 34520, 33552, 33274, 30330, 30066],-->
<!--  'TARAVAL': [13897, 12510, 14022, 13545, 13526, 12067, 12082, 12617, 12954, 13502, 12635, 12104],-->
<!--  'TENDERLOIN': [16958, 15285, 16921, 15819, 15965, 14543, 15186, 16210, 15565, 15826, 14633, 14043],-->
<!--  'ALL':[178056,161560,179035,172294,176420,168232,175525,181183,176413,183034,168193,164521]-->
<!--};-->
<!--export default {-->
<!--  props:['area'],-->
<!--  name: "history",-->
<!--  data() {-->
<!--    return {-->
<!--      option: null,-->
<!--      number: 0, // 播放所在下标-->
<!--      timer: null,-->
<!--      xData: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],-->
<!--      data :[]-->
<!--    };-->
<!--  },-->
<!--  mounted() {-->
<!--    this.getEchart();-->
<!--    this.startAutoPlay();-->
<!--    this.initializeData();-->
<!--  },-->
<!--  watch: {-->
<!--    area(newArea) {-->
<!--      this.updateBusinessData(newArea);-->
<!--    },-->
<!--  },-->
<!--  methods: {-->
<!--    initializeData() {-->
<!--      if (this.area && this.data[this.area]) {-->
<!--        this.data = ALL_AREA_DATA[this.area];-->
<!--      } else {-->

<!--        this.data = ALL_AREA_DATA['ALL'];-->
<!--      }-->
<!--    },-->
<!--    updateBusinessData(newArea) {-->
<!--      if (newArea && this.data[newArea]) {-->
<!--        this.data = ALL_AREA_DATA[newArea];-->
<!--      } else {-->
<!--        // 如果 newArea 不存在，设置为默认值-->
<!--        this.data = ALL_AREA_DATA['ALL'];-->
<!--      }-->
<!--      // 更新图表-->
<!--      this.updateChart();-->
<!--    },-->
<!--    getEchart() {-->
<!--      let myChart = echarts.init(document.getElementById('chart_arc'));-->
<!--      this.option = {-->
<!--        tooltip: {-->
<!--          trigger: 'axis',-->
<!--          showContent: false,-->
<!--          axisPointer: {-->
<!--            type: 'shadow',-->
<!--            shadowStyle: {-->
<!--              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{-->
<!--                offset: 1,-->
<!--                color: '#5d83ff'-->
<!--              },{-->
<!--                offset: 0,-->
<!--                color: 'rgba(255, 255, 255, 0)'-->
<!--              }])-->
<!--            }-->
<!--          },-->
<!--        },-->
<!--        color: ['#5d83ff'],-->
<!--        grid: {-->
<!--          top: 30,-->
<!--          left: 20,-->
<!--          right: 20,-->
<!--          bottom: 20,-->
<!--          containLabel: true // 轴上的数值-->
<!--        },-->
<!--        xAxis: {-->
<!--          type: 'category',-->
<!--          data: this.xData,-->
<!--          boundaryGap: false,-->
<!--          axisTick: {-->
<!--            show: false-->
<!--          },-->
<!--          axisLabel: {-->
<!--            formatter: '{value} 月'-->
<!--          },-->
<!--          axisLine: {-->
<!--            lineStyle: {-->
<!--              color: '#999',-->
<!--            }-->
<!--          },-->
<!--        },-->
<!--        yAxis: {-->
<!--          type: 'value',-->
<!--          axisLine: {-->
<!--            show: false,-->
<!--            lineStyle: {-->
<!--              color: '#999'-->
<!--            }-->
<!--          },-->
<!--        },-->
<!--        series: [{-->
<!--          name: '人数',-->
<!--          type: 'line',-->
<!--          data: this.data,-->
<!--          symbolSize: 10,-->
<!--          itemStyle: {-->
<!--            opacity: 0,-->
<!--          },-->
<!--          emphasis: {-->
<!--            label: {-->
<!--              show: true,-->
<!--              color: '#fff',-->
<!--              fontSize: 20-->
<!--            },-->
<!--            itemStyle: {-->
<!--              color: '#5d83ff',-->
<!--              borderColor: '#fff',-->
<!--              borderWidth: 2,-->
<!--              opacity: 1-->
<!--            },-->
<!--          },-->
<!--          areaStyle: {-->
<!--            normal: {-->
<!--              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{-->
<!--                offset: 0,-->
<!--                color: '#5d83ff'-->
<!--              },{-->
<!--                offset: 1,-->
<!--                color: 'rgba(0, 0, 0, 0)'-->
<!--              }]),-->
<!--            }-->
<!--          },-->
<!--          smooth: true,-->
<!--        }]-->
<!--      };-->
<!--      myChart.setOption(this.option, true);-->

<!--      window.addEventListener('resize', () => {-->
<!--        myChart.resize();-->
<!--      });-->

<!--      // 保存 chart 实例以便销毁时使用-->
<!--      this.myChart = myChart;-->
<!--    },-->
<!--    startAutoPlay() {-->
<!--      this.timer = setInterval(() => {-->
<!--        this.myChart.dispatchAction({-->
<!--          type: 'showTip',-->
<!--          seriesIndex: 0,-->
<!--          dataIndex: this.number-->
<!--        });-->

<!--        this.number++;-->

<!--        if (this.number >= this.data.length) {-->
<!--          this.number = 0;-->
<!--        }-->
<!--      }, 1000);-->
<!--    }-->
<!--  },-->
<!--  beforeDestroy() {-->
<!--    if (this.timer) {-->
<!--      clearInterval(this.timer);-->
<!--    }-->
<!--    if (this.myChart) {-->
<!--      this.myChart.dispose();-->
<!--    }-->
<!--  }-->
<!--};-->
<!--</script>-->

<!--<style lang="scss" scoped>-->
<!--.history-container {-->
<!--  position: relative;-->
<!--  width: 100%; // 设定宽度为父级的 100%-->
<!--  height: 100%; // 确定容器高度-->
<!--  margin: 0 auto;-->

<!--  .wrap-container.sn-container {-->
<!--    position: relative;-->
<!--    margin-left: -19px;-->
<!--    width: 107%;-->
<!--    height: 99%;-->
<!--    display: flex; // 使用 Flex 布局使内容居中-->
<!--    align-items: center;-->
<!--    justify-content: center;-->

<!--    .sn-content {-->
<!--      .sn-title {-->
<!--        font-size: 1.2rem;-->
<!--        color: #fff;-->
<!--        text-align: center;-->
<!--        margin-bottom: 20px;-->
<!--      }-->
<!--      .sn-body {-->
<!--        .chartsdom {-->
<!--          width: 100%;-->
<!--          height: 80%;-->
<!--        }-->
<!--      }-->
<!--    }-->
<!--  }-->
<!--}-->
<!--</style>-->
<template>
  <div class="history-container">
    <div class="wrap-container sn-container">
      <div class="sn-content">
        <div class="sn-title"></div>
        <div class="sn-body">
          <div class="wrap-container">
            <div class="chartsdom" id="chart_arc"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import * as echarts from 'echarts';

// 定义所有区域的数据常量
const ALL_AREA_DATA = {
  'BAYVIEW': [18645, 16697, 18338, 17159, 17426, 16293, 17015, 17484, 16844, 17728, 16243, 15608],
  'CENTRAL': [19414, 17380, 19288, 19000, 18189, 17741, 19504, 18994, 18293, 19246, 17181, 17693],
  'INGLESIDE': [16200, 15281, 16628, 15718, 15155, 13886, 14612, 14736, 14911, 15672, 14139, 14154],
  'MISSION': [26172, 23413, 25678, 24749, 24464, 22687, 23375, 24345, 23919, 25023, 23345, 21815],
  'NORTHERN': [24205, 21491, 23696, 22699, 22196, 20786, 22222, 22497, 21169, 22698, 21429, 21347],
  'PARK': [10561, 9385, 10619, 10802, 10209, 9429, 9658, 10257, 9967, 10370, 9606, 8835],
  'RICHMOND': [9867, 9144, 10093, 9902, 9873, 8927, 9033, 9523, 9239, 9695, 8652, 8856],
  'SOUTHERN': [33803, 30539, 34106, 32855, 32936, 31873, 32838, 34520, 33552, 33274, 30330, 30066],
  'TARAVAL': [13897, 12510, 14022, 13545, 13526, 12067, 12082, 12617, 12954, 13502, 12635, 12104],
  'TENDERLOIN': [16958, 15285, 16921, 15819, 15965, 14543, 15186, 16210, 15565, 15826, 14633, 14043],
  'ALL': [178056, 161560, 179035, 172294, 176420, 168232, 175525, 181183, 176413, 183034, 168193, 164521]
};

export default {
  props: ['area'],
  name: "history",
  data() {
    return {
      option: null,
      number: 0, // 播放所在下标
      timer: null,
      xData: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
      data: [] // 当前显示的数据
    };
  },
  mounted() {
    // 1. 初始化 data
    this.initializeData();
    // 2. 初始化图表
    this.getEchart();
    // 3. 启动自动播放
    this.startAutoPlay();
  },
  watch: {
    area(newArea) {
      this.updateBusinessData(newArea);
    },
  },
  methods: {
    // 初始化当前数据，基于传入的 area 属性
    initializeData() {
      if (this.area && ALL_AREA_DATA[this.area]) {
        this.data = ALL_AREA_DATA[this.area];
      } else {
        // 设置一个默认区域的数据，例如 'ALL'
        this.data = ALL_AREA_DATA['ALL'];
      }
      console.log('Initialized data:', this.data);
    },
    // 根据新的 area 更新 data 的值
    updateBusinessData(newArea) {
      if (newArea && ALL_AREA_DATA[newArea]) {
        this.data = ALL_AREA_DATA[newArea];
      } else {
        // 如果 newArea 不存在，设置为默认区域的数据
        this.data = ALL_AREA_DATA['ALL'];
      }
      console.log('Updated data:', this.data);
      // 更新图表
      this.updateChart();
    },
    // 初始化 ECharts 实例
    getEchart() {
      // 初始化 ECharts 实例
      const chart = echarts.init(document.getElementById('chart_arc'));
      this.option = {
        tooltip: {
          trigger: 'axis',
          showContent: false,
          axisPointer: {
            type: 'shadow',
            shadowStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                offset: 1,
                color: '#5d83ff'
              }, {
                offset: 0,
                color: 'rgba(255, 255, 255, 0)'
              }])
            }
          },
        },
        color: ['#5d83ff'],
        grid: {
          top: 30,
          left: 20,
          right: 20,
          bottom: 20,
          containLabel: true // 轴上的数值
        },
        xAxis: {
          type: 'category',
          data: this.xData,
          boundaryGap: false,
          axisTick: {
            show: false
          },
          axisLabel: {
            formatter: '{value} '
          },
          axisLine: {
            lineStyle: {
              color: '#999',
            }
          },
        },
        yAxis: {
          type: 'value',
          axisLine: {
            show: false,
            lineStyle: {
              color: '#999'
            }
          },
        },
        series: [{
          name: '人数',
          type: 'line',
          data: this.data,
          symbolSize: 10,
          itemStyle: {
            opacity: 0,
          },
          emphasis: {
            label: {
              show: true,
              color: '#fff',
              fontSize: 20
            },
            itemStyle: {
              color: '#5d83ff',
              borderColor: '#fff',
              borderWidth: 2,
              opacity: 1
            },
          },
          areaStyle: {
            normal: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                offset: 0,
                color: '#5d83ff'
              }, {
                offset: 1,
                color: 'rgba(0, 0, 0, 0)'
              }]),
            }
          },
          smooth: true,
        }]
      };
      chart.setOption(this.option, true);

      // 保存 chart 实例以便后续更新和销毁
      this.myChart = chart;

      // 监听窗口大小变化，动态调整图表大小
      window.addEventListener('resize', () => {
        this.myChart.resize();
      });
    },
    // 更新 ECharts 图表的数据
    updateChart() {
      if (this.myChart) {
        this.myChart.setOption({
          series: [{
            data: this.data
          }]
        });
      }
    },
    // 启动自动播放逻辑
    startAutoPlay() {
      this.timer = setInterval(() => {
        if (this.myChart) {
          this.myChart.dispatchAction({
            type: 'showTip',
            seriesIndex: 0,
            dataIndex: this.number
          });

          this.number++;

          if (this.number >= this.data.length) {
            this.number = 0;
          }
        }
      }, 1000); // 每秒更新一次
    }
  },
  beforeDestroy() {
    // 清除定时器
    if (this.timer) {
      clearInterval(this.timer);
    }
    // 销毁 ECharts 实例
    if (this.myChart) {
      this.myChart.dispose();
    }
  }
};
</script>

<style lang="scss" scoped>
.history-container {
  position: relative;
  width: 100%; // 设定宽度为父级的 100%
  height: 100%; // 确定容器高度
  margin: 0 auto;

  .wrap-container.sn-container {
    position: relative;
    margin-left: -19px;
    width: 107%;
    height: 99%;
    display: flex; // 使用 Flex 布局使内容居中
    align-items: center;
    justify-content: center;

    .sn-content {
      .sn-title {
        font-size: 1.2rem;
        color: #fff;
        text-align: center;
        margin-bottom: 20px;
      }
      .sn-body {
        .chartsdom {
          width: 100%;
          height: 80%;
        }
      }
    }
  }
}
</style>
