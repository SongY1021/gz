<template>
  <view
    :class="'icon-' + type"
    :style="{ color: color, 'font-size': size + 'px' }"
    class="fonticon"
    @click="_onClick"
  />
</template>

<script>
export default {
  name: 'fontIcon',
  props: {
    type: {
      type: String,
      default: ''
    },
    color: {
      type: String,
      default: '#333333'
    },
    size: {
      type: [Number, String],
      default: 16
    }
  },
  methods: {
    _onClick () {
      this.$emit('click')
    }
  }
}
</script>

<style>
@font-face {
	 font-family: "iconfont";
    src: url('//at.alicdn.com/t/font_1506000_4v2a0w7e8ls.eot');
    src: url('//at.alicdn.com/t/font_1506000_4v2a0w7e8ls.eot?#iefix') format('embedded-opentype'),
    url('//at.alicdn.com/t/font_1506000_4v2a0w7e8ls.woff2') format('woff2'),
    url('//at.alicdn.com/t/font_1506000_4v2a0w7e8ls.woff') format('woff'),
    url('//at.alicdn.com/t/font_1506000_4v2a0w7e8ls.ttf') format('truetype'),
    url('//at.alicdn.com/t/font_1506000_4v2a0w7e8ls.svg#iconfont') format('svg');
}

.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.uni-icon-wrapper {
	line-height: 1;
}
.iconfont.uni-active {
	color: #007aff;
}
.icon-50:before {
  content: "\e632";
}

.icon-jia:before {
  content: "\e61a";
}

.icon-sousuo:before {
  content: "\e643";
}

.icon-zijinmingxi:before {
  content: "\e640";
}

.icon-shaixuan:before {
  content: "\e6d9";
}

.icon-qiandaijinbi:before {
  content: "\e602";
}

.icon-tubiao:before {
  content: "\e60e";
}

.icon-sousuo1:before {
  content: "\e6cc";
}

.icon-sousuo2:before {
  content: "\e700";
}

.icon-fuhao-shaixuan:before {
  content: "\e728";
}

.icon-sousuo3:before {
  content: "\e759";
}

.icon-shouqian-cuxiantiao:before {
  content: "\e687";
}

.icon-shouqian-cuxiantiao1:before {
  content: "\e68e";
}

.icon-shouru:before {
  content: "\e64d";
}

.icon-sousuo4:before {
  content: "\e604";
}

.icon-wanglaimingxizhang:before {
  content: "\e60a";
}

.icon-zhanghushouru:before {
  content: "\e60c";
}

.icon-qianbao:before {
  content: "\e6ca";
}

.icon-shengchengshouruquerendan:before {
  content: "\e674";
}

.icon-tubiao1:before {
  content: "\e648";
}

.icon-17:before {
  content: "\e61f";
}

.icon-tubiao-copy:before {
  content: "\e75a";
}

.icon-50-copy:before {
  content: "\e75b";
}

.icon-50-copy-copy:before {
  content: "\e75c";
}

.icon-tubiao-copy-copy:before {
  content: "\e75d";
}

</style>
