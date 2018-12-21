<template>
  <div>
    <div id="echart2" ref="echart2"></div>
    <div>{{show}}</div>
  </div>
</template>
<script>
export default {
  name: "echart2",
  data() {
    return {
      aadata: [],
      bbdata: [],
      ccdata: [],
      zydata: [],
      show: []
    };
  },
  mounted() {
    var that = this;
   /*  var e = [1, 2, 3, 4];
    console.log(e.splice(e.indexOf(2), 1));
    console.log(e); */
    var aa = Math.random();
    var cc = [];
    for (var i = 0; i < 100; i++) {
      that.aadata.push(aa);
      that.bbdata.push(i);
      cc.push(0);
    }
    cc.splice(cc.length - 1, 1, that.aadata[that.aadata.length - 1]);
    that.ccdata = cc;
    that.api();
    setInterval(function() {
      that.api();
    }, 1000);
  },
 /*  watch: {
    xdata(re) {
      this.drawLine();
    }
  }, */
  methods: {
  api() {
      var that = this;
      var obj = { CodeID: ["2"] };
      that.$axios
        .post(
          "http://112.64.170.158:9111/Service1.svc/RealTimeData",
          JSON.stringify(obj),
          { headers: { "Content-Type": "application/json;" } }
        )
        .then(res => {
          var that = this;
          that.show = res.data.Item;
          var b = res.data.Item[0];
          that.aadata.shift();
          /*   .shift() */
          that.bbdata.shift();
          that.aadata.push(b);
          that.bbdata.push(b);
          console.log(that.aadata);
          console.log(that.aadata);
          that.ccdata.splice(that.zydata.length - 1, 1, b);
          console.log(that.zydata);
          /* that.$set(that.xdata.shift()); */
          that.drawLine();
          console.log(res);
        })
        .catch(error => {
          console.log(error);
        });
    },
    drawLine() {
      var that = this;
      var myChart = this.$echarts.init(this.$refs.echart2);
      myChart.setOption({
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: that.bbdata
        },
        yAxis: {
          type: "value"
          /* max: 0.5 */
        },
        series: [
          {
            data: that.aadata,
            type: "line",
             animation: false,
            smooth: true,
            symbol: "none",
            lineStyle: {
              color: {
                type: "linear",
                /*   x: 0,
    y: 0,
    x2: 0,
    y2: 1, */
                colorStops: [
                  {
                    offset: 0,
                    color: "#0eb92e" // 0% 处的颜色
                  },
                  {
                    offset: 0.8,
                    color: "#0eb92e" // 0% 处的颜色
                  },
                  {
                    offset: 1,
                    color: "#f0e242" // 100% 处的颜色
                  }
                ],
                opacity: 0.4,
                globalCoord: false // 缺省为 false
              }
            }
          },
          {
            name: "最高气温",
            barWidth: 2,
            type: "bar",
            data: that.ccdata,
            animation: false,
           /*  markPoint: {
              animation: false,
              symbol: "emptyCircle",
              data: [{ type: "max" }],
              symbolSize: 16,
              itemStyle: {
                normal: {
                  label: {
                    show: false
                  }
                }
              }
            } */
          }
        ]
      });
    }
  }
};
</script>
<style scoped>
#echart2 {
  width: 500px;
  height:300px;
}
</style>
