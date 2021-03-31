<template>
  <!-- 旅游数据分析页面S -->
  <div class="page-data">
    <!-- 页面顶部S -->
    <div class="head">
      <h1>新疆旅游各项数据图表</h1>
      <!-- 倒计时 -->
      <p class="show-time">{{ time }}</p>
    </div>
    <!-- 页面顶部E -->
    <!-- 页面数据部分S -->
    <div class="box-data">
      <!-- 左侧数据部分S -->
      <div class="box-3 box-left">
        <!-- 左侧柱状图S -->
        <div class="box echarts-bar1">
          <h2>新疆旅游景点TOP10</h2>
          <div class="year">
            <a
              href="javascript:;"
              :class="selectY == 2020 ? 'active' : ''"
              @click="selectYear(2020)"
              >2020年</a
            >
            <a
              href="javascript:;"
              :class="selectY == 2019 ? 'active' : ''"
              @click="selectYear(2019)"
              >2019年</a
            >
          </div>
          <div class="chart"></div>
          <div class="border-footer"></div>
        </div>
        <!-- 左侧柱状图E -->
        <!-- 左侧折线图S -->
        <div class="box echarts-line1">
          <h2>新疆2019年与2020年个月旅游人次</h2>
          <div class="chart"></div>
          <div class="border-footer"></div>
        </div>
        <!-- 左侧折线图E -->
        <!-- 左侧饼图S -->
        <div class="box echarts-pie1">
          <h2>人均消费/天</h2>
          <div class="chart"></div>
          <div class="border-footer"></div>
        </div>
        <!-- 左侧饼图E -->
      </div>
      <!-- 左侧数据部分E -->
      <!-- 中间数据部分S -->
      <div class="box-center">
        <!-- 上方数字S -->
        <div class="num">
          <ul>
            <li class="after">325811</li>
            <li>184563</li>
          </ul>
          <div>
            <p>实时进入新疆人数</p>
            <p>实时离开新疆人数</p>
          </div>
        </div>
        <!-- 上方数字E -->
        <!-- 下方地图S -->
        <div class="map">
          <div class="chart"></div>
          <div class="bg1"></div>
          <div class="bg2"></div>
          <div class="bg3"></div>
        </div>
        <!-- 下方地图E -->
      </div>
      <!-- 中间数据部分E -->
      <!-- 右侧数据部分S -->
      <div class="box-3 box-right">
        <!-- 右侧柱状图S -->
        <div class="box echarts-bar2">
          <h2>2020全年新疆旅游年龄区间人次</h2>
          <div class="chart"></div>
          <div class="border-footer"></div>
        </div>
        <!-- 右侧柱状图E -->
        <!-- 右侧折线图S -->
        <div class="box echarts-line2">
          <h2>新疆2019-2020年自驾游与跟团游图表</h2>
          <div class="chart"></div>
          <div class="border-footer"></div>
        </div>
        <!-- 右侧折线图E -->
        <!-- 右侧饼图S -->
        <div class="box echarts-pie2">
          <h2>2020全年游客地区分布TOP10</h2>
          <div class="chart"></div>
          <div class="border-footer"></div>
        </div>
        <!-- 右侧饼图E -->
      </div>
      <!-- 右侧数据部分E -->
    </div>
    <!-- 页面数据部分E -->
  </div>
  <!-- 页面结束E -->
</template>
<script>
export default {
  data() {
    return {
      time: "",
      timer: null,
      selectY: 2020,
    };
  },
  methods: {
    // 获取时间S
    getTime() {
      clearTimeout(this.timer); //清除已有定时器
      let t = new Date(); //创建当前时间
      let y = t.getFullYear(); //获取年
      let mt = t.getMonth() + 1; //获取月
      let day = t.getDate(); //获取日
      let h = t.getHours(); //获取时
      let m = t.getMinutes(); //获取分
      let s = t.getSeconds(); //获取秒
      if (h < 10) {
        h = "0" + h;
      } else if (m < 10) {
        m = "0" + m;
      } else if (s < 10) {
        s = "0" + s;
      }
      this.time = `当前时间： ${y}年${mt}月${day}日-${h}时${m}分${s}秒`;
      this.timer = setTimeout(this.getTime, 100);
    },
    // 获取时间E
    //左侧柱状图数据S
    echartsBar1() {
      let data = [
        [
          198238,
          291827,
          88986,
          120731,
          397281,
          319281,
          401271,
          221829,
          162571,
          118271,
        ],
        [
          128372,
          138721,
          129831,
          98271,
          208161,
          382918,
          452918,
          128721,
          82716,
          192711,
        ],
      ];
      let ydata = [];
      if (this.selectY == 2020) {
        ydata = data[0];
      } else {
        ydata = data[1];
      }
      let myChart = echarts.init(
        document.querySelector(
          ".page-data .box-data .box-3 .echarts-bar1 .chart"
        )
      );
      let option = {
        color: ["#2f89cf"],
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "shadow",
          },
        },
        grid: {
          left: "0%",
          top: "10px",
          right: "0%",
          bottom: "4%",
          containLabel: true,
        },
        xAxis: [
          {
            type: "category",
            data: [
              "喀纳斯",
              "禾木",
              "五彩滩",
              "赛里木湖",
              "那拉提",
              "巴音布鲁克",
              "天山天池",
              "火焰山",
              "坎儿井",
              "吐鲁番",
            ],
            axisTick: {
              alignWithLabel: true,
            },
            axisLabel: {
              textStyle: {
                color: "rgba(255,255,255,.6)",
                fontSize: "12",
              },
            },
            axisLine: {
              show: false,
            },
          },
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              textStyle: {
                color: "rgba(255,255,255,.6)",
                fontSize: "12",
              },
            },
            axisLine: {
              lineStyle: {
                color: "rgba(255,255,255,.1)",
              },
            },
            splitLine: {
              lineStyle: {
                color: "rgba(255,255,255,.1)",
              },
            },
          },
        ],
        series: [
          {
            name: "旅游人次",
            type: "bar",
            barWidth: "35%",
            data: ydata,
            itemStyle: {
              barBorderRadius: 5,
            },
          },
        ],
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    //左侧柱状图数据E
    //左侧折线图S
    echartsLine1() {
      let myChart = echarts.init(
        document.querySelector(
          ".page-data .box-data .box-3 .echarts-line1 .chart"
        )
      );
      let data = {
        year: [
          [
            98129,
            120893,
            159287,
            239171,
            482719,
            781011,
            982316,
            1002376,
            739217,
            928317,
            328172,
            112938,
          ],
          [
            193728,
            162736,
            172361,
            288927,
            402718,
            828371,
            1283278,
            1492712,
            928371,
            982371,
            492813,
            228173,
          ],
        ],
      };
      let option = {
        color: ["#00f2f1", "#ed3f35"],
        tooltip: {
          trigger: "axis",
        },
        legend: {
          right: "10%",
          textStyle: {
            color: "#4c9bfd",
            fontSize: "10",
          },
        },
        grid: {
          top: "20%",
          left: "3%",
          right: "4%",
          bottom: "3%",
          show: true,
          borderColor: "#012f4a",
          containLabel: true,
        },

        xAxis: {
          type: "category",
          boundaryGap: false,
          data: [
            "1月",
            "2月",
            "3月",
            "4月",
            "5月",
            "6月",
            "7月",
            "8月",
            "9月",
            "10月",
            "11月",
            "12月",
          ],
          axisTick: {
            show: false,
          },
          axisLabel: {
            color: "rgba(255,255,255,.7)",
          },
          axisLine: {
            show: false,
          },
        },
        yAxis: {
          type: "value",
          axisTick: {
            show: false,
          },
          axisLabel: {
            color: "rgba(255,255,255,.7)",
          },
          splitLine: {
            lineStyle: {
              color: "#012f4a",
            },
          },
        },
        series: [
          {
            name: "2019年新疆旅游总人次",
            type: "line",
            smooth: true,
            data: data.year[0],
          },
          {
            name: "2020年新疆旅游总人次",
            type: "line",
            smooth: true,
            data: data.year[1],
          },
        ],
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    // 左侧折线图E
    //左侧饼图S
    echartsPie1() {
      let myChart = echarts.init(
        document.querySelector(
          ".page-data .box-data .box-3 .echarts-pie1 .chart"
        )
      );
      let option = {
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b}: {c} ({d}%)",
          position: function (p) {
            return [p[0] + 10, p[1] - 10];
          },
        },
        legend: {
          top: "90%",
          itemWidth: 10,
          itemHeight: 10,
          data: [
            "¥50-¥200",
            "¥200-¥500",
            "¥500-¥800",
            "¥800-¥1500",
            "¥1500以上",
          ],
          textStyle: {
            color: "rgba(255,255,255,.5)",
            fontSize: "8",
          },
        },
        series: [
          {
            name: "人均消费/天",
            type: "pie",
            center: ["50%", "42%"],
            radius: ["40%", "70%"],
            color: ["#d8d9f0", "#787ce4", "#3036d4", "#242542", "#020427"],
            label: { show: false },
            labelLine: { show: false },
            data: [
              { value: 48, name: "¥50-¥200" },
              { value: 194, name: "¥200-¥500" },
              { value: 228, name: "¥500-¥800" },
              { value: 102, name: "¥800-¥1500" },
              { value: 88, name: "¥1500以上" },
            ],
          },
        ],
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    //左侧饼图E
    // 中间地图S
    echartsMap() {
      let myChart = echarts.init(
        document.querySelector(".page-data .box-data .box-center .map .chart")
      );
      let geoCoordMap = {
        上海: [121.4648, 31.2891],
        东莞: [113.8953, 22.901],
        东营: [118.7073, 37.5513],
        中山: [113.4229, 22.478],
        临汾: [111.4783, 36.1615],
        临沂: [118.3118, 35.2936],
        丹东: [124.541, 40.4242],
        丽水: [119.5642, 28.1854],
        乌鲁木齐: [87.9236, 43.5883],
        佛山: [112.8955, 23.1097],
        保定: [115.0488, 39.0948],
        兰州: [103.5901, 36.3043],
        包头: [110.3467, 41.4899],
        北京: [116.4551, 40.2539],
        北海: [109.314, 21.6211],
        南京: [118.8062, 31.9208],
        南宁: [108.479, 23.1152],
        南昌: [116.0046, 28.6633],
        南通: [121.1023, 32.1625],
        厦门: [118.1689, 24.6478],
        台州: [121.1353, 28.6688],
        合肥: [117.29, 32.0581],
        呼和浩特: [111.4124, 40.4901],
        咸阳: [108.4131, 34.8706],
        哈尔滨: [127.9688, 45.368],
        唐山: [118.4766, 39.6826],
        嘉兴: [120.9155, 30.6354],
        大同: [113.7854, 39.8035],
        大连: [122.2229, 39.4409],
        天津: [117.4219, 39.4189],
        太原: [112.3352, 37.9413],
        威海: [121.9482, 37.1393],
        宁波: [121.5967, 29.6466],
        宝鸡: [107.1826, 34.3433],
        宿迁: [118.5535, 33.7775],
        常州: [119.4543, 31.5582],
        广州: [113.5107, 23.2196],
        廊坊: [116.521, 39.0509],
        延安: [109.1052, 36.4252],
        张家口: [115.1477, 40.8527],
        徐州: [117.5208, 34.3268],
        德州: [116.6858, 37.2107],
        惠州: [114.6204, 23.1647],
        成都: [103.9526, 30.7617],
        扬州: [119.4653, 32.8162],
        承德: [117.5757, 41.4075],
        拉萨: [91.1865, 30.1465],
        无锡: [120.3442, 31.5527],
        日照: [119.2786, 35.5023],
        昆明: [102.9199, 25.4663],
        杭州: [119.5313, 29.8773],
        枣庄: [117.323, 34.8926],
        柳州: [109.3799, 24.9774],
        株洲: [113.5327, 27.0319],
        武汉: [114.3896, 30.6628],
        汕头: [117.1692, 23.3405],
        江门: [112.6318, 22.1484],
        沈阳: [123.1238, 42.1216],
        沧州: [116.8286, 38.2104],
        河源: [114.917, 23.9722],
        泉州: [118.3228, 25.1147],
        泰安: [117.0264, 36.0516],
        泰州: [120.0586, 32.5525],
        济南: [117.1582, 36.8701],
        济宁: [116.8286, 35.3375],
        海口: [110.3893, 19.8516],
        淄博: [118.0371, 36.6064],
        淮安: [118.927, 33.4039],
        深圳: [114.5435, 22.5439],
        清远: [112.9175, 24.3292],
        温州: [120.498, 27.8119],
        渭南: [109.7864, 35.0299],
        湖州: [119.8608, 30.7782],
        湘潭: [112.5439, 27.7075],
        滨州: [117.8174, 37.4963],
        潍坊: [119.0918, 36.524],
        烟台: [120.7397, 37.5128],
        玉溪: [101.9312, 23.8898],
        珠海: [113.7305, 22.1155],
        盐城: [120.2234, 33.5577],
        盘锦: [121.9482, 41.0449],
        石家庄: [114.4995, 38.1006],
        福州: [119.4543, 25.9222],
        秦皇岛: [119.2126, 40.0232],
        绍兴: [120.564, 29.7565],
        聊城: [115.9167, 36.4032],
        肇庆: [112.1265, 23.5822],
        舟山: [122.2559, 30.2234],
        苏州: [120.6519, 31.3989],
        莱芜: [117.6526, 36.2714],
        菏泽: [115.6201, 35.2057],
        营口: [122.4316, 40.4297],
        葫芦岛: [120.1575, 40.578],
        衡水: [115.8838, 37.7161],
        衢州: [118.6853, 28.8666],
        西宁: [101.4038, 36.8207],
        西安: [109.1162, 34.2004],
        贵阳: [106.6992, 26.7682],
        连云港: [119.1248, 34.552],
        邢台: [114.8071, 37.2821],
        邯郸: [114.4775, 36.535],
        郑州: [113.4668, 34.6234],
        鄂尔多斯: [108.9734, 39.2487],
        重庆: [107.7539, 30.1904],
        金华: [120.0037, 29.1028],
        铜川: [109.0393, 35.1947],
        银川: [106.3586, 38.1775],
        镇江: [119.4763, 31.9702],
        长春: [125.8154, 44.2584],
        长沙: [113.0823, 28.2568],
        长治: [112.8625, 36.4746],
        阳泉: [113.4778, 38.0951],
        青岛: [120.4651, 36.3373],
        韶关: [113.7964, 24.7028],
      };

      var XAData = [
        [{ name: "乌鲁木齐" }, { name: "北京", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "上海", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "广州", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "西宁", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "拉萨", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "郑州", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "呼和浩特", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "福州", value: 100 }],
      ];

      var XNData = [
        [{ name: "乌鲁木齐" }, { name: "北京", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "武汉", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "上海", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "广州", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "西安", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "银川", value: 100 }],
        [{ name: "上海" }, { name: "乌鲁木齐", value: 100 }],
        [{ name: "广州" }, { name: "乌鲁木齐", value: 100 }],
        [{ name: "武汉" }, { name: "乌鲁木齐", value: 100 }],
        [{ name: "北京" }, { name: "乌鲁木齐", value: 100 }],
        [{ name: "沈阳" }, { name: "乌鲁木齐", value: 100 }],
        [{ name: "郑州" }, { name: "乌鲁木齐", value: 100 }],
        [{ name: "拉萨" }, { name: "乌鲁木齐", value: 100 }],
        [{ name: "福州" }, { name: "乌鲁木齐", value: 100 }],
        [{ name: "呼和浩特" }, { name: "乌鲁木齐", value: 100 }],
      ];

      var YCData = [
        [{ name: "乌鲁木齐" }, { name: "北京", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "潍坊", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "哈尔滨", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "青岛", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "沈阳", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "重庆", value: 100 }],
        [{ name: "乌鲁木齐" }, { name: "贵阳", value: 100 }],
      ];

      var planePath =
        "path://M1705.06,1318.313v-89.254l-319.9-221.799l0.073-208.063c0.521-84.662-26.629-121.796-63.961-121.491c-37.332-0.305-64.482,36.829-63.961,121.491l0.073,208.063l-319.9,221.799v89.254l330.343-157.288l12.238,241.308l-134.449,92.931l0.531,42.034l175.125-42.917l175.125,42.917l0.531-42.034l-134.449-92.931l12.238-241.308L1705.06,1318.313z";
      //var planePath = 'arrow';
      var convertData = function (data) {
        var res = [];
        for (var i = 0; i < data.length; i++) {
          var dataItem = data[i];

          var fromCoord = geoCoordMap[dataItem[0].name];
          var toCoord = geoCoordMap[dataItem[1].name];
          if (fromCoord && toCoord) {
            res.push({
              fromName: dataItem[0].name,
              toName: dataItem[1].name,
              coords: [fromCoord, toCoord],
              value: dataItem[1].value,
            });
          }
        }
        return res;
      };

      var color = ["#fff", "#fff", "#fff"]; //航线的颜色
      var series = [];
      [
        ["乌鲁木齐", XAData],
        ["乌鲁木齐", XNData],
        ["乌鲁木齐", YCData],
      ].forEach(function (item, i) {
        series.push(
          {
            name: item[0] + " Top3",
            type: "lines",
            zlevel: 1,
            effect: {
              show: true,
              period: 6,
              trailLength: 0.7,
              color: "red", //arrow箭头的颜色
              symbolSize: 3,
            },
            lineStyle: {
              normal: {
                color: color[i],
                width: 0,
                curveness: 0.2,
              },
            },
            data: convertData(item[1]),
          },
          {
            name: item[0] + " Top3",
            type: "lines",
            zlevel: 2,
            symbol: ["none", "arrow"],
            symbolSize: 10,
            effect: {
              show: true,
              period: 6,
              trailLength: 0,
              symbol: planePath,
              symbolSize: 15,
            },
            lineStyle: {
              normal: {
                color: color[i],
                width: 1,
                opacity: 0.6,
                curveness: 0.2,
              },
            },
            data: convertData(item[1]),
          },
          {
            name: item[0] + " Top3",
            type: "effectScatter",
            coordinateSystem: "geo",
            zlevel: 2,
            rippleEffect: {
              brushType: "stroke",
            },
            label: {
              normal: {
                show: true,
                position: "right",
                formatter: "{b}",
              },
            },
            symbolSize: function (val) {
              return val[2] / 8;
            },
            itemStyle: {
              normal: {
                color: color[i],
              },
              emphasis: {
                areaColor: "#2B91B7",
              },
            },
            data: item[1].map(function (dataItem) {
              return {
                name: dataItem[1].name,
                value: geoCoordMap[dataItem[1].name].concat([
                  dataItem[1].value,
                ]),
              };
            }),
          }
        );
      });
      var option = {
        tooltip: {
          trigger: "item",
          formatter: function (params, ticket, callback) {
            if (params.seriesType == "effectScatter") {
              return "线路：" + params.data.name + "" + params.data.value[2];
            } else if (params.seriesType == "lines") {
              return (
                params.data.fromName +
                ">" +
                params.data.toName +
                "<br />" +
                params.data.value
              );
            } else {
              return params.name;
            }
          },
        },

        geo: {
          map: "china",
          label: {
            emphasis: {
              show: true,
              color: "#fff",
            },
          },
          roam: false,
          zoom: 1,
          itemStyle: {
            normal: {
              areaColor: "rgba(43, 196, 243, 0.42)",
              borderColor: "rgba(43, 196, 243, 1)",
              borderWidth: 1,
            },
            emphasis: {
              areaColor: "#2B91B7",
            },
          },
        },
        series: series,
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    // 中间地图E
    // 右侧柱状图S
    echartsBar2() {
      let myChart = echarts.init(
        document.querySelector(
          ".page-data .box-data .box-3 .echarts-bar2 .chart"
        )
      );

      let titlename = ["0-18岁", "18-30岁", "30-45岁", "45-60岁", "60岁以上"];
      let valdata = ["152万", "432万", "287万", "187万", "118万"];
      let data = [1522928, 4328178, 2873132, 1873218, 1189232];
      let myColor = ["#1089E7", "#F57474", "#56D0E3", "#F8B448", "#8B78F6"];
      let option = {
        grid: {
          top: "10%",
          left: "18%",
          bottom: "10%",
          right: "11%",
        },
        xAxis: {
          show: false,
        },
        yAxis: [
          {
            show: true,
            data: titlename,
            inverse: true,
            axisLine: {
              show: false,
            },
            splitLine: {
              show: false,
            },
            axisTick: {
              show: false,
            },
            axisLabel: {
              color: "#fff",

              rich: {
                lg: {
                  backgroundColor: "#339911",
                  color: "#fff",
                  borderRadius: 15,
                  align: "center",
                  width: 15,
                  height: 15,
                },
              },
            },
          },
          {
            show: true,
            inverse: true,
            data: valdata,
            axisLabel: {
              textStyle: {
                fontSize: 10,
                color: "#fff",
              },
            },
          },
        ],
        series: [
          {
            name: "条",
            type: "bar",
            yAxisIndex: 0,
            data: data,
            barCategoryGap: 50,
            barWidth: 10,
            itemStyle: {
              normal: {
                barBorderRadius: 20,
                color: function (params) {
                  var num = myColor.length;
                  return myColor[params.dataIndex % num];
                },
              },
            },
            label: {
              normal: {
                show: true,
                position: "inside",
                formatter: "{c}",
              },
            },
          },
          {
            name: "框",
            type: "bar",
            yAxisIndex: 1,
            barCategoryGap: 50,
            data: [4800000, 4800000, 4800000, 4800000, 4800000],
            barWidth: 15,
            itemStyle: {
              normal: {
                color: "none",
                borderColor: "#00c1de",
                borderWidth: 3,
                barBorderRadius: 15,
              },
            },
          },
        ],
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    // 右侧柱状图E
    // 右侧折线图S
    echartsLine2() {
      let myChart = echarts.init(
        document.querySelector(
          ".page-data .box-data .box-3 .echarts-line2 .chart"
        )
      );
      let option = {
        tooltip: {
          trigger: "axis",
          axisPointer: {
            lineStyle: {
              color: "#dddc6b",
            },
          },
        },
        legend: {
          top: "0%",
          textStyle: {
            color: "rgba(255,255,255,.5)",
            fontSize: "12",
          },
        },
        grid: {
          left: "10",
          top: "30",
          right: "10",
          bottom: "10",
          containLabel: true,
        },

        xAxis: [
          {
            type: "category",
            boundaryGap: false,
            axisLabel: {
              textStyle: {
                color: "rgba(255,255,255,.6)",
                fontSize: 12,
              },
            },
            axisLine: {
              lineStyle: {
                color: "rgba(255,255,255,.2)",
              },
            },

            data: [
              "201901月",
              "201902月",
              "201903月",
              "201904月",
              "201905月",
              "201906月",
              "201907月",
              "201908月",
              "201909月",
              "201911月",
              "201912月",
              "202001月",
              "202002月",
              "202003月",
              "202004月",
              "202005月",
              "202006月",
              "202007月",
              "202008月",
              "202009月",
              "202011月",
              "202012月",
            ],
          },
          {
            axisPointer: { show: false },
            axisLine: { show: false },
            position: "bottom",
            offset: 20,
          },
        ],

        yAxis: [
          {
            type: "value",
            axisTick: { show: false },
            axisLine: {
              lineStyle: {
                color: "rgba(255,255,255,.1)",
              },
            },
            axisLabel: {
              textStyle: {
                color: "rgba(255,255,255,.6)",
                fontSize: 12,
              },
            },

            splitLine: {
              lineStyle: {
                color: "rgba(255,255,255,.1)",
              },
            },
          },
        ],
        series: [
          {
            name: "跟团游(万人次)",
            type: "line",
            smooth: true,
            symbol: "circle",
            symbolSize: 5,
            showSymbol: false,
            lineStyle: {
              normal: {
                color: "#0184d5",
                width: 2,
              },
            },
            areaStyle: {
              normal: {
                color: new echarts.graphic.LinearGradient(
                  0,
                  0,
                  0,
                  1,
                  [
                    {
                      offset: 0,
                      color: "rgba(1, 132, 213, 0.4)",
                    },
                    {
                      offset: 0.8,
                      color: "rgba(1, 132, 213, 0.1)",
                    },
                  ],
                  false
                ),
                shadowColor: "rgba(0, 0, 0, 0.1)",
              },
            },
            itemStyle: {
              normal: {
                color: "#0184d5",
                borderColor: "rgba(221, 220, 107, .1)",
                borderWidth: 12,
              },
            },
            data: [
              8.2,
              6.7,
              12.5,
              15,
              7,
              27.9,
              28.0,
              31.2,
              20.5,
              28.7,
              19.8,
              26.7,
              8.8,
              9.2,
              7.7,
              14.5,
              17,
              7,
              29.9,
              30.0,
              33.2,
              22.5,
              26.7,
              21.8,
              24.7,
              9.8,
            ],
          },
          {
            name: "自驾游(万人次)",
            type: "line",
            smooth: true,
            symbol: "circle",
            symbolSize: 5,
            showSymbol: false,
            lineStyle: {
              normal: {
                color: "#00d887",
                width: 2,
              },
            },
            areaStyle: {
              normal: {
                color: new echarts.graphic.LinearGradient(
                  0,
                  0,
                  0,
                  1,
                  [
                    {
                      offset: 0,
                      color: "rgba(0, 216, 135, 0.4)",
                    },
                    {
                      offset: 0.8,
                      color: "rgba(0, 216, 135, 0.1)",
                    },
                  ],
                  false
                ),
                shadowColor: "rgba(0, 0, 0, 0.1)",
              },
            },
            itemStyle: {
              normal: {
                color: "#00d887",
                borderColor: "rgba(221, 220, 107, .1)",
                borderWidth: 12,
              },
            },
            data: [
              11.2,
              9.8,
              8.9,
              17.9,
              30.9,
              33.0,
              37.2,
              19.5,
              31.7,
              21.8,
              28.7,
              18.8,
              12.2,
              5.7,
              19.5,
              15,
              7,
              32.9,
              37.0,
              28.2,
              24.5,
              31.7,
              17.8,
              21.7,
              11.8,
            ],
          },
        ],
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    // 右侧折线图E
    // 右侧饼图S
    echartsPie2() {
      let myChart = echarts.init(
        document.querySelector(
          ".page-data .box-data .box-3 .echarts-pie2 .chart"
        )
      );
      let option = {
        legend: {
          top: "90%",
          itemWidth: 10,
          itemHeight: 10,
          textStyle: {
            color: "rgba(255,255,255,.5)",
            fontSize: "12",
          },
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)",
        },
        color: [
          "#006cff",
          "#60cda0",
          "#ed8884",
          "#ff9f7f",
          "#0096ff",
          "#9fe6b8",
          "#32c5e9",
          "#fff",
          "#46c4af",
          "#9a9c23",
        ],
        series: [
          {
            name: "游客地区统计(万人次)",
            type: "pie",
            radius: ["5%", "75%"],
            center: ["50%", "42%"],
            roseType: "radius",
            data: [
              { value: 8.23, name: "云南" },
              { value: 22.76, name: "北京" },
              { value: 16.35, name: "山东" },
              { value: 9.72, name: "河北" },
              { value: 12.9, name: "江苏" },
              { value: 14.41, name: "浙江" },
              { value: 11.69, name: "深圳" },
              { value: 5.75, name: "四川" },
              { value: 20.61, name: "新疆" },
              { value: 17.69, name: "河南" },
            ],
            label: {
              fontSize: 10,
            },
            labelLine: {
              length: 3,
              length2: 10,
            },
          },
        ],
      };
      myChart.setOption(option);
      window.addEventListener("resize", function () {
        myChart.resize();
      });
    },
    // 右侧饼图E
    //左侧柱状图年份切换S
    selectYear(year) {
      this.selectY = year;
      this.echartsBar1();
    },
    //左侧柱状图年份切换E
  },
  mounted() {
    this.getTime(); //调用获取时间函数
    this.echartsBar1(); //加载左侧柱状图
    this.echartsLine1(); //加载左侧折线图
    this.echartsPie1(); //加载左侧饼图
    this.echartsBar2(); //加载右侧柱状图
    this.echartsLine2(); //加载右侧折线图
    this.echartsPie2(); //加载右侧饼图
    this.echartsMap(); 
  },
};
</script>