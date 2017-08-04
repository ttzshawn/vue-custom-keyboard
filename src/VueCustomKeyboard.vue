<template>
  <div>
    <div v-if="isOpen" class="keyboardMask" @click="onBlur" onTouchMove={this.preventTouchMove}></div>
  
    <div class="keyboard" :class="{keyboardOpen: this.isOpen}" onTouchMove={this.preventTouchMove} :style="{height: `${winH * 0.32}px`}">
      <div :class="{keyboardLayout: true, hide: this.inputValue.length >= 1}">
        <span v-for="(item, i) in level1" :key="i" class="btnKey">
          <button class="button" type="button" @click="e => selectLevel1(e, item)">
            {{item}}
          </button>
          <div class="btnActive">
            <span>{{item}}</span>
          </div>
        </span>
      </div>
      <div :class="{keyboardLayout: true, hide: true, show: this.inputValue.length >= 1}">
        <span v-for="(item, i) in level2" :key="i" class="btnKey">
          <button class="button" type="button" @click="e => selectLevel2(e, item)">
            {{item}}
          </button>
          <div class="btnActive">
            <span>{{item}}</span>
          </div>
        </span>
        <span class="btnKey backspace">
          <button class="button" type="button" @click="backspace">
            <i class="iconfont icon-backspace"></i>
          </button>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isOpen: {
      type: Boolean,
      default: true
    },
    level1: {
      type: String,
      default: '粤京津泸鲁冀云辽黑湘皖新苏浙赣鄂桂甘晋蒙陕吉闽贵青藏川宁琼豫渝台港澳'
    },
    level2: {
      type: String,
      default: '1234567890QWERTYUPASDFGHJKLZXCVBNM'
    },
    maxLength: {
      type: Number,
      default: 7
    },
    onChange: {
      type: Function,
      default: (onChangeFunc) => {
        onChangeFunc(this.inputValue);
      }
    },
    done: {
      type: Function,
      default: () => {
        this.isOpen = false;
      }
    },
    defaultValue: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      winH: window.innerHeight,
      inputValue: this.defaultValue || ''
    };
  },
  watch: {
    defaultValue() {
      this.inputValue = this.defaultValue;
    }
  },
  methods: {
    selectLevel1(e, level1) {
      e.preventDefault();
      this.inputValue = level1;
      this.onChange(level1);
    },
    selectLevel2(e, level2) {
      e.preventDefault();
      const inputValue = this.inputValue + level2;

      if (inputValue.length > this.maxLength) {
        this.done();
      } else {
        this.inputValue = inputValue;
        this.onChange(inputValue);
      }
    },
    backspace() {
      const inputValue = this.inputValue;
      const backspaceValue = inputValue.substr(0, inputValue.length - 1);

      this.inputValue = backspaceValue;
      this.onChange(backspaceValue);
    },
    onBlur() {
      this.isOpen = false;
    }
  }
};
</script>

<style lang="scss">
@font-face {
  font-family: "iconfont";
  src: url('./font/iconfont.woff') format('woff'),
  url('./font/iconfont.ttf') format('truetype'),
  url('./font/iconfont.svg#iconfont') format('svg');
}

.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -webkit-text-stroke-width: 0.2px;
  -moz-osx-font-smoothing: grayscale;
}

.icon-backspace:before {
  content: "\e600";
}

.keyboardMask {
  position: absolute;
  z-index: 100;
  top: 36px;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: transparent;
}

.keyboard {
  position: fixed;
  z-index: 900;
  right: 0;
  bottom: 0;
  left: 0;
  padding-top: 6px;
  user-select: none;
  transition: transform 200ms ease-out;
  transform: translateY(100%);
  text-align: center;
  background-color: #dedfe0;
}

.keyboardOpen {
  transform: translateY(0);
}

.keyboardLayout {
  height: 100%;
}

.btnKey {
  position: relative;
  display: inline-block;
  width: 10%;
  height: 25%;
}

.button {
  font-size: 14px;
  display: inline;
  width: 80%;
  height: 80%;
  margin: 10% auto;
  padding: 0;
  text-align: center;
  border: 0;
  border-radius: 3px;
  background-color: #fff;
  box-shadow: 0 2px 3px rgba(0, 0, 0, .15);
  &:focus {
    outline: 0;
  }
  &:active~.btnActive {
    font-size: 16px;
    line-height: 200%;
    position: absolute;
    top: 0;
    left: -10%;
    display: table;
    width: 120%;
    height: 100%;
    margin-bottom: 10px;
    transform: translateY(-100%);
    border-radius: 5px;
    background-color: #fff;
    box-shadow: 0 2px 3px rgba(0, 0, 0, .15);
    span {
      display: table-cell;

      width: 100%;

      text-align: center;
      vertical-align: middle;
    }
    &::after {
      position: absolute;
      bottom: 0;
      left: 50%;

      width: 0;
      height: 0;

      content: '';
      transform: translate3d(-50%, 100%, 0);

      border-top: 10px solid #fff;
      border-right: 10px solid transparent;
      border-left: 10px solid transparent;
    }
  }
  i {
    font-size: 28px !important;
    color: #fff;
  }
}

.btnActive {
  display: none;
}

.hide {
  display: none;
}

.show {
  display: block;
}

.backspace {
  width: 15%;
  vertical-align: middle;
  i {
    font-size: 20px;
  }
  .button {
    background-color: #cbcdd1;
    &:active {
      background-color: #fff;
      i {
        color: #cbcdd1;
      }
    }
  }
}

.keyboardHide {
  display: none;
}

.keyboardShow {
  display: block;
}
</style>
