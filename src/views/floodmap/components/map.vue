<template>
  <div class="amap-page-container">
    <el-amap
      vid="amapDemo"
      :center="center"
      :zoom="zoom"
      :events="events"
      :amap-manager="amapManager"
      :plugin="plugin"
      class="amap-demo"
    >
      <!-- 遍历显示 -->
      <el-amap-marker
        v-for="marker in markers"
        :position="marker.position"
        :events="marker.events"
      ></el-amap-marker>
    </el-amap>

    <div class="toolbar">
      position: [{{ lng }}, {{ lat }}] address: {{ address }}
      <button type="button" name="button" v-on:click="addMarker">
        add markers
      </button>
      <button type="button" name="button" v-on:click="removeMarker">
        remove markers
      </button>
    </div>
  </div>
</template>

  <style>
.amap-page-container {
  width: 100%;
  height: 500px;
}
</style>

  <script>
// NPM 方式
import { AMapManager } from "vue-amap";
import VueAMap from "vue-amap";
//import AMap from 'AMap'

let amapManager = new VueAMap.AMapManager();

export default {
  name: "mmap",
  data: function () {
    let self = this;

    return {
      //*******************地图和组件初始化设置**********************//
      amapManager,
      zoom: 12,
      center: [121.59996, 31.197646],
      data_position : [
        // 只能使用position
        {position: [121.59996, 31.197646]},
        {position: [121.69996, 31.197646]},
        {position: [121.79996, 31.197646]},
        {position: [121.89996, 31.197646]},
        {position: [121.99996, 31.197646]},
      ],

      address: "",
      markers: [],
      events: {
        init(o) {
          o.getCity((result) => {
            //result 为地图初始化时所在位置的行政区域信息
            console.log(result);
          });
        },

        //*******************鼠标点击产生确定地址**********************//
        click(e) {
          let { lng, lat } = e.lnglat;
          self.lng = lng;
          self.lat = lat;
          //这里是通过高德地图 SDK 完成的
          var geocoder = new AMap.Geocoder({
            radius: 1000,
            extensions: "all",
          });
          var position_xy = [lng, lat];
          console.log(position_xy);

          //*****************在鼠标点击处添加标注点*******************//
          if (self.markers.length);
          self.markers.splice(self.markers.length - 1, 1);
          let marker = {
            position: [lng, lat],
          };
          self.markers.push(marker);

          geocoder.getAddress(position_xy, function (status, result) {
            //console.log(result)
            if (status === "complete" && result.info === "OK") {
              if (result && result.regeocode) {
                self.address = result.regeocode.formattedAddress;
                console.log(self.address);
                self.$nextTick();
              }
            }
          });
        },

        // //鼠标在点标记上按下时触发事件
        // mousedown() {
        //   var a = "hahaha";
        //   console.log(a);
        // },
      },

      lng: 0,
      lat: 0,
      //*******************卫星+路网+路况**********************//
      plugin: [
        "ToolBar",
        {
          pName: "MapType",
          defaultType: 0,
          events: {
            init(o) {
              //console.log(o);
            },
          },
        },
      ],
    };
  },

  //*******************在地图上添加点**********************//
  methods: {
    addMarker() {
      // console.log(this.data_position);
      for (let x of this.data_position)
      {
        this.markers.push(x);
      }
      console.log(this.markers);
    },
    removeMarker() {
      if (!this.markers.length) return;
      this.markers.splice(this.markers.length - 1, 1);
    },
  },
};
</script>
