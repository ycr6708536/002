<template lang="pug">
canvas
</template>

<script>
export default {
  ready () {
    this.init()
    setInterval(this.draw, 33)
    window.onresize = this.init
  },
  data () {
    return {
      character: '田由甲申甴电甶男甸甹町画甼甽甾甿畀畁畂畃畄畅畆畇畈畉畊畋界畍畎畏畐畑',
      context: '',
      unitWidth: 0,
      columnHeight: []
    }
  },
  methods: {
    init () {
      this.width = this.$el.width = this.$el.offsetWidth
      this.height = this.$el.height = this.$el.offsetHeight
      this.context = this.$el.getContext('2d')
      this.unitWidth = parseInt(window.getComputedStyle(this.$el, false)['fontSize'])
      this.initColumnHeight(1)
    },
    initColumnHeight (val) {
      /* eslint-disable curly */
      for (let i = 0, j = this.width / this.unitWidth; i < j; i++)
        this.columnHeight.push(val)
      /* eslint-enable curly */
    },
    draw () {
      this.drawReact()
      this.drawRow()
    },
    drawReact () {
      this.context.fillStyle = 'rgba(0, 0, 0, .05)'
      this.context.fillRect(0, 0, this.width, this.height)
    },
    drawRow () {
      for (let i = 0, j = this.columnHeight.length; i < j; i++) {
        this.drawColumn(i)
        /* eslint-disable curly */
        if (this.shouldReset(i))
          this.columnHeight[i] = 0
        /* eslint-enable curly */
        this.columnHeight[i]++
      }
    },
    drawColumn (index) {
      this.context.fillStyle = '#0f0'
      this.context.font = `${this.unitWidth}px arial`
      this.context.fillText(this.randomText(), index * this.unitWidth, this.columnHeight[index] * this.unitWidth)
    },
    shouldReset (index) {
      return this.columnHeight[index] * this.unitWidth > this.height && Math.random() < 0.016
    },
    randomText () {
      let num = Math.floor(Math.random() * this.character.length)
      return this.character.charAt(num)
    }
  }
}
</script>

<style lang="sass" scoped>
canvas
  position: absolute
  left: 0; top: 0
  width: 100%; height: 100%
  background: #000
