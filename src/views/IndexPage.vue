<template>
  <div>
    <input type="text" v-model="value" />
    <div class="contain-box">
      <digital-keyboard
        :value="value"
        @updateKey="handleUpdateKey"
      ></digital-keyboard>
    </div>
  </div>
</template>

<script>
import DigitalKeyboard from '@/components/DigitalKeyboard.vue'
export default {
  name: 'IndexPage',
  components: { DigitalKeyboard },
  data () {
    return {
      value: ''
    }
  },
  methods: {
    handleUpdateKey (val) {
      this.value = val
    }
  }
}
</script>

<style lang="scss">
.contain-box {
  display: flex;
  justify-content: center;
  margin-top: 50px;
}
</style>
