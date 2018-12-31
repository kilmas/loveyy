<template>
<div>
  <map
    :center.sync="center"
    :zoom.sync="zoom"
    :map-type-id.sync="mapType"
    @g-click="mapClick()"
    >
    <marker
      v-if="showIcon"
      :position.sync="Icon"
      :icon.sync="icon"
      @g-click="center = LA"
    ></marker>
    <marker
      v-if="mkvisible"
      :position.sync="mposition"
      @g-click="center = mposition"
    ></marker>
    <marker
      v-if="LAvisible"
      :position.sync="LA"
      @g-click="center = LA"
    ></marker>
    <marker
      v-if="Fvisible"
      :position.sync="Fairbanks"
      @g-click="center = Fairbanks"
    ></marker>

    <info-window
    v-if="infowin"
    :position.sync="infoWP"
    :opened.sync="infowin"
    >
      {{{info}}}
    </info-window>

    <polyline v-if="plvisible" :path.sync="plPath" :options="{geodesic:true, strokeColor:'#FF0000'}">
    </polyline>
    
  </map>

</div>
</template>

<script>
import {load, Marker, Map, Cluster, InfoWindow, Polyline, Rectangle, Circle, Polygon, PlaceInput} from 'vue-google-maps'

load('AIzaSyDvw8wuIuika2GitdeO-qJJkEKDe3s32I0', '', ['places'], true)

export default {
  data: function data () {
    return {
      info: '',
      showIcon: false,
      mkvisible: false,
      LAvisible: false,
      Fvisible: false,
      infoWin: '',
      infowin: false,
      infoWP: {lat: 23.0471681521, lng: 113.1254234346},
      icon: {url: 'http://qingah.com/src/assets/airplane.png'},
      plane: require('../assets/plane.png'),
      infoWinP: {lat: 23.0471681521, lng: 113.1254234346},
      mposition: {lat: 23.0471681521, lng: 113.1254234346},
      Foshan: {lat: 23.0471681521, lng: 113.1254234346},
      center: {lat: 23.0471681521, lng: 113.1254234346},
      Icon: {lat: 23.0471681521, lng: 113.1254234346},
      LA: {lat: 33.9415889000, lng: -118.4085300000},
      Fairbanks: {lat: 64.8377360070, lng: -147.7159881592},
      University: {lat: 64.8487420000, lng: -147.8134585000},
      Wiseman: {lat: 67.4100000000, lng: -150.1074999000},
      DaltonHighway: {lat: 67.8442387000, lng: -149.8169965000},
      line: {
        foshan: {lat: 23.0471681521, lng: 113.1254234346},
        guangzhou: {lat: 23.40085, lng: 113.312942},
        la: {lat: 33.9415889000, lng: -147.7159881592},
        Fairbanks: {lat: 64.8377360070, lng: -147.7159881592},
        Wiseman: {lat: 67.4100000000, lng: 150.1074999000},
        University: {lat: 64.8487420000, lng: -147.8134585000},
        NorthPole: {lat: 64.8487420000, lng: -147.8134585000},
        DaltonHighway: {lat: 67.8442387000, lng: -149.8169965000}
      },
      carLoad: [
        {lat: 67.5222234267, lng: -149.8507690430},
        {lat: 67.6353619276, lng: -149.7656250000},
        {lat: 67.7593981320, lng: -149.7518920898},
        {lat: 67.8858832206, lng: -149.8260498047},
        {lat: 67.9921375426, lng: -149.7491455078},
        {lat: 68.0999556780, lng: -149.5266723633},
        {lat: 68.2103301692, lng: -149.4085693359},
        {lat: 68.3445137681, lng: -149.3289184570},
        {lat: 68.4930196118, lng: -149.4497680664},
        {lat: 68.6355527137, lng: -149.5294189453},
        {lat: 68.7214373340, lng: -148.9828491211},
        {lat: 69.6799895091, lng: -148.7109375000},
        {lat: 70.2140611493, lng: -148.4082984924}
      ],
      zoom: 0,
      gridSize: 50,
      mapType: 'roadmap', // ROADMAP
      markers: [
        [{
          position: {lat: 23.0471681521, lng: 113.1254234346}
        }, {
          position: {lat: 23.40085, lng: 113.312942}
        }]
      ],
      markersEven: false,
      // mapStyle: 'green',
      plPath: [
        {lat: 23.0471681521, lng: 113.1254234346},
        {lat: 33.9415889000, lng: -118.4085300000}
        // {lat: 64.8377360070, lng: -147.7159881592}
      ],
      plvisible: false,
      pictureHtml: [
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/Wiseman/1.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/Wiseman/2.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/DaltonHighway/1.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/DaltonHighway/2.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/DaltonHighway/3.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/DaltonHighway/4.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/DaltonHighway/5.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/Wiseman/3.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/Wiseman/4.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/Fairbanks/1.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/Fairbanks/2.jpg">',
        '<br/><img style="width:100%" src="http://qingah.com/src/assets/Fairbanks2/1.jpg">'
      ],
      carPic: [
        {lat: 67.5144121170, lng: -149.8503398895},
        {lat: 67.6305279667, lng: -149.7760963440},
        {lat: 67.7475050041, lng: -149.7603034970},
        {lat: 67.8765434167, lng: -149.8227024078},
        {lat: 67.9801374511, lng: -149.7636508942},
        {lat: 68.0899651872, lng: -149.5508766174},
        {lat: 68.1963710980, lng: -149.4152641296},
        {lat: 68.3133255367, lng: -149.3550109863},
        {lat: 68.3464141078, lng: -149.3381881701},
        {lat: 68.6055152941, lng: -149.5362854004},
        {lat: 68.7029899890, lng: -149.0515136725},
        {lat: 69.6570265969, lng: -148.7023544305},
        {lat: 70.2004301825, lng: -148.4098434448}
      ]
    }
  },

  filters: {
    markerRemover (markers) {
      if (this.markersEven) {
        const result = []
        for (let i = 0; i < markers.length; i += 2) {
          result.push(markers[i])
        }
        return result
      } else {
        return markers
      }
    }
  },

  computed: {
    mapStyles () {
      switch (this.mapStyle) {
        case 'normal':
          return []
        case 'red':
          return [{stylers: [{hue: '#890000'}, {visibility: 'simplified'}, {gamma: 0.5}, {weight: 0.5}]},
          {elementType: 'labels', stylers: [{visibility: 'off'}]},
          {featureType: 'water', stylers: [{color: '#890000'}]}]
        default:
          return [{stylers: [{hue: '#899999'}, {visibility: 'on'}, {gamma: 0.5}, {weight: 0.5}]},
              {featureType: 'road', stylers: [{visibility: 'off'}]},
              {featureType: 'transit.line', stylers: [{color: '#FF0000'}]},
              {featureType: 'poi', elementType: 'labels.icon', stylers: [{visibility: 'on'}, {weight: 10}]},
              {featureType: 'water', stylers: [{color: '#8900FF'}, {weight: 9999900000}]}]
      }
    }
  },
  ready () {
    this.zoomTo(12, 1000, this.toFoShan)
  },
  methods: {
    mapClick () {

    },
    zoomTo (zoom, time, callback, point) {
      // let map = {}
      time = time || 1000
      let loop = null
      let seft = this
      let loopZoom = function () {
        // let curZoom = map.getZoom()
        // console.log('test')
        let curZoom = seft.zoom
        if (curZoom === zoom) {
          // console.log(curZoom)
          clearTimeout(loop)
          callback = callback || function () {}
          callback()
          return false
        }
        seft.mkvisible = false
        seft.mkvisible = true
        let plus = curZoom > zoom ? -1 : 1
        let toZoom = curZoom + plus
        // map.setZoom(toZoom)
        seft.zoom = toZoom
        if (point) {
          seft.center = point
        }
        loop = setTimeout(loopZoom, time)
      }
      loopZoom()
    },
    showPic (time, callback, point) {
      time = time || 6000
      let loop = null
      let length = this.pictureHtml.length
      let i = 0
      let seft = this
      seft.zoom = 12
      this.icon = {url: 'http://qingah.com/src/assets/car.png'}
      let loopPic = function () {
        if (i === length) {
          clearTimeout(loop)
          callback = callback || function () {}
          callback()
          setTimeout(function () {
            seft.all()
          }, 6000)
          return false
        }
        seft.center = seft.carLoad[i]
        seft.infoWP = seft.carLoad[i]
        seft.Icon = seft.carPic[i]
        seft.info = seft.pictureHtml[i]
        seft.infowin = true
        i++
        if (point) {
          seft.center = point
        }
        loop = setTimeout(loopPic, time)
      }
      loopPic()
    },
    toFoShan (callback) {
      let seft = this
      this.infowin = true
      this.info = 'Is your Home? I want to take you see the aurora borealis.'
      // to world
      setTimeout(function () {
        seft.infowin = false
        callback = callback || function () {}
        callback()
        seft.zoomTo(1, 1000, seft.world)
      }, 8000)
    },
    world (callback) {
      let seft = this
      setTimeout(function () {
        seft.maKerLA()
      }, 2000)
    },
    makerF () {
      this.Fvisible = true
      let seft = this
      setTimeout(function () {
        seft.icon = {url: 'http://qingah.com/src/assets/airplane1.png'}
        seft.fly(seft.destination, [seft.LA, {lat: 49.2678046600, lng: -120.1464843750}, {lat: 60.3269477430, lng: -133.0664062500}, {lat: 64.8377360070, lng: -147.7159881592}])
      }, 2000)
    },
    destination () {
      this.infoWP = this.Fairbanks
      this.info = 'This is Fairbanks,destination'
      this.infowin = true
      let seft = this
      setTimeout(function () {
        seft.zoom = 15
        seft.infowin = false
        seft.fairbanks()
      }, 5000)
    },
    daltonHighway () {
      this.info = '<br/><img style="width:100%" src="http://qingah.com/src/assets/DaltonHighway/1.jpg">'
      this.infowin = true
      let seft = this
      setTimeout(function () {
        seft.infoWP = seft.DaltonHighway
        seft.center = seft.DaltonHighway
        seft.showPic()
      }, 5000)
    },
    fairbanks () {
      this.info = '<br/><img style="width:100%" src="http://qingah.com/src/assets/Wiseman/5.jpg">'
      this.infowin = true
      let seft = this
      setTimeout(function () {
        seft.infoWP = seft.Fairbanks
        seft.center = seft.Fairbanks
        this.info = '<br/><img style="width:100%" src="http://qingah.com/src/assets/Fairbanks/7.jpg">'
        seft.wiseman()
      }, 5000)
    },
    wiseman () {
      this.info = '<br/><img style="width:100%" src="http://qingah.com/src/assets/Fairbanks2/1.jpg">'
      this.infowin = true
      let seft = this
      setTimeout(function () {
        seft.infoWP = seft.Wiseman
        seft.center = seft.Wiseman
        seft.info = '<br/><img style="width:100%" src="http://qingah.com/src/assets/Fairbanks2/2.jpg">'
        seft.university()
      }, 5000)
    },
    university () {
      let seft = this
      setTimeout(function () {
        seft.infoWP = seft.University
        seft.center = seft.University
        this.info = '<br/><img style="width:100%" src="http://qingah.com/src/assets/University/1.jpg">'
        seft.daltonHighway()
      }, 5000)
    },
    maKerLA (callback) {
      this.LAvisible = true
      this.drawLine(null)
      let seft = this
      setTimeout(function () {
        seft.center = seft.LA
        let audio = document.getElementById('myAudio')
        audio.play()
        seft.fly(seft.showLA, [{lat: 23.0471681521, lng: 113.1254234346},
        {lat: 30.4486736793, lng: 131.3086044788},
        {lat: 37.1603165467, lng: 157.8515732288},
        {lat: 43.7075935041, lng: -172.6171767712},
        {lat: 45.4601344006, lng: -146.6015517712},
        {lat: 33.9415889000, lng: -118.4085300000}])
      }, 3000)
    },
    showLA (callback) {
      this.info = 'This is Los Angeles International Airport (LAX),and transfer Fairbanks'
      this.infoWP = this.LA
      this.infowin = true
      let seft = this
      setTimeout(function () {
        seft.center = seft.LA
        seft.infowin = false
        seft.makerF()
        seft.drawLine(null, {lat: 64.8377360070, lng: -147.7159881592})
      }, 5000)
    },
    fly (callback) {
      // let xab = LocA.lat-LocB.lat
      // let yab = LocA.lng-LocB.lng
      // let AB = Math.sqrt(xab * xab + yab * yab)
      // infoWinP
      this.showIcon = true
      let seft = this
      let length = arguments[1].length
      let i = 0
      let arg = arguments[1]
      let loop = null
      let loopFly = function () {
        if (i === length) {
          callback = callback || function () {}
          callback()
          clearTimeout(loop)
          return false
        }
        // console.log(arg)
        seft.center = arg[i]
        seft.Icon = arg[i]
        seft.zoom = 3
        i++
        loop = setTimeout(loopFly, 2000)
      }
      loopFly()
    },
    drawLine (callback, line) {
      this.plvisible = true
      if (line) {
        this.plPath.push(line)
      }
      callback = callback || function () {}
      setTimeout(callback, 2000)
    },
    all () {
      this.$dispatch('all')
    }
  },
  components: {
    Map,
    Marker,
    Cluster,
    InfoWindow,
    Polygon,
    Polyline,
    Rectangle,
    Circle,
    PlaceInput
  },
  watch: {
    // center (center) {
    //   console.log(center)
    // }
  }
}
</script>

<style>
map {
  width:100%;
  height: 600px;
  display: block;
}
</style>
