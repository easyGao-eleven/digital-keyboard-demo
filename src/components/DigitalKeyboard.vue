<template>
  <div class="keyboard">
    <div class="keyboard_key">
      <div class="keyboard_number" @click="handleKeyPress">
        <div class="pos-right-pad-num">
          <button
            type="button"
            class="pad-num"
            :data-num="item"
            v-for="(item, index) in numArr"
            :key="index"
          >
            {{ item }}
          </button>
          <button type="button" class="pad-num--max" data-num="0">0</button>
          <button type="button" class="pad-num" data-num=".">.</button>
        </div>
      </div>
      <div class="pos-right-pad-act" @click="handleExecBtnPress">
        <button
          type="button"
          class="pad-num special-key border-right exit"
          data-num="exit"
        >
          退出
        </button>
        <button
          type="button"
          class="pad-num special-key border-right del"
          data-num="del"
        >
          退格
        </button>
        <button
          type="button"
          class="pad-num special-key border-right clear-all"
          data-num="delAll"
        >
          清空
        </button>
        <button
          type="button"
          class="pad-num special-key border-right sure"
          data-num="sure"
        >
          确定
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      defaultValue: '',
      numArr: ['1', '2', '3', '4', '5', '6', '7', '8', '9']
    }
  },
  props: {
    value: {
      type: String,
      default: ''
    },
    // 最大输入长度
    maxLength: {
      type: Number,
      default: 10
    }
  },
  created () {
    this.getDefaultValue()
  },
  methods: {
    getDefaultValue () {
      this.defaultValue = this.value
    },
    handleKeyPress (e) {
      const num = e.target.dataset.num
      this.addNum(num)
      this.$emit('updateKey', this.defaultValue)
    },
    handleExecBtnPress (e) {
      const num = e.target.dataset.num
      if (num) {
        if (num === 'sure') {
          this.$emit('sureKey', this.defaultValue)
          return
        }
        if (num === 'exit') {
          this.$emit('clickHide')
          return
        }
        switch (String(num)) {
          case 'delAll':
            this.deleteAllKey()
            break
          case 'del':
            this.deleteKey()
            break
          default:
            this.addNum(num)
            break
        }
        this.$emit('updateKey', this.defaultValue)
      }
    },
    deleteKey () {
      const values = this.defaultValue
      if (!values.length) {
        return false
      } else {
        this.defaultValue = values.substring(0, values.length - 1)
        this.$emit('updateKey', this.defaultValue)
      }
    },
    deleteAllKey () {
      this.defaultValue = ''
      this.$emit('updateKey', this.defaultValue)
    },
    addNum (num) {
      const value = this.defaultValue
      this.defaultValue = value + num
    }
  }
}
</script>
<style lang="scss" scoped>
.keyboard {
  width: 400px;
  height: 350px;
  background: #dbdbdb;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr=#99000000,endColorstr=#99000000);
  box-shadow: 0 0 10px rgb(43, 42, 42);
  padding: 20px;
  border-radius: 10px;
  user-select: none;
  -ms-user-select: none;
  button {
    background-color: aliceblue;
  }
}
.keyboard_key {
  padding-top: 10px;
  width: 95%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.keyboard_number {
  display: flex;
  width: 75%;
  margin: 0;
  padding: 0;
  vertical-align: bottom;
  flex-direction: row;
  justify-content: space-between;
  flex-wrap: wrap;
  align-items: center;
}
.pos-right-pad-num {
  display: flex;
  width: 100%;
  flex-wrap: wrap;
}
.pos-right-pad-act {
  width: 25%;
}
.pad-num {
  width: 60px;
  height: 60px;
  line-height: 60px;
  text-align: center;
  background: #fff;
  border-radius: 10px;
  font-weight: bold;
  margin: 10px;
  float: left;
  box-shadow: 0px 2px 1px #000;
  color: #000;
  font-size: 24px;
  cursor: pointer;
}
.pad-num--max {
  width: 140px;
  height: 60px;
  line-height: 60px;
  text-align: center;
  background: #fff;
  border-radius: 10px;
  font-weight: bold;
  margin: 10px;
  float: left;
  box-shadow: 0px 2px 1px #000;
  color: #000;
  font-size: 24px;
  cursor: pointer;
}
.exit {
  color: #f44336;
}
.del {
  color: #ff9800;
}
.clear--all {
  color: #2196f3;
}
.sure {
  width: 190px;
  color: #4caf50;
}
.special-key {
  background: #fff;
  width: 100%;
}
</style>
