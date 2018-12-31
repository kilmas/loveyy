<template>
<div id="mainDiv">
    <div id="content">
        <div id="code">
            {{{html}}}
        </div>
    </div>
    <div class="bottom" v-if="ok" @click="go">
      <img src="http://qingah.com/src/assets/start.png">
    </div>
</div>
</template>

<script>
import html from './LoveYY.html'
export default {
  data () {
    return {
      msg: 'Hello World!',
      html: '',
      ok: false
    }
  },
  methods: {
    writer () {
      let typeWriter = document.getElementById('typeWriter')
      let str = html
      let progress = 0
      let self = this
      let timer = setInterval(function () {
        let current = str.substr(progress, 1)
        if (current === '<') {
          progress = str.indexOf('>', progress) + 1
        } else {
          progress++
        }
        typeWriter.play()
        self.html = (str.substring(0, progress) + (progress & 1 ? '_' : ''))
        if (progress >= str.length) {
          typeWriter.pause()
          self.ok = true
          clearInterval(timer)
        }
      }, 75)
    },
    go () {
      this.$dispatch('greeting')
    }
  },
  ready () {
    let seft = this
    setTimeout(function () {
      seft.writer()
    }, 3000)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
#mainDiv{
	width: 100%;
	height: 100%;
}
#content {
	height: 100%;
  padding: 10px;
}

#code {
	color: #333;
	font-family: "Consolas", "Monaco", "Bitstream Vera Sans Mono", "Courier New", "sans-serif";
	font-size: 12px;
}

#code .string{
	color: #2a36ff;
}

#code .keyword{
	color: #7f0055;
	font-weight:bold;
}

#code .placeholder{
	margin-left:15px;
}

#code .space{
	margin-left:7px;
}

#code .comments{
	color: #3f7f5f;
}

#errorMsg{
	width: 100%;
	text-align: center;
	font-size: 24px;
	position: absolute;
	top: 100px;
	left:0px;
}
.bottom {
    position:fixed;
    bottom: 0px;
    width: 100%;
    text-align:center;
    padding:10px;
    font-size: 30px;
}
</style>
