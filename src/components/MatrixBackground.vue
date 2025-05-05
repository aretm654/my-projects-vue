<template>
  <div class="grid-background" ref="container">
    <div 
      v-for="(line, index) in lines" 
      :key="index" 
      class="grid-line" 
      :style="getLineStyle(line)"
    ></div>
  </div>
</template>

<script>
export default {
  name: 'GridBackground',
  props: {
    lineCount: {
      type: Number,
    },
    speed: {
      type: Number,
    },
    cellSize: {
      type: Number,
    },
    lineColor: {
      type: String,
    },
    lineThickness: {
      type: Number,
    }
  },
  data() {
    return {
      container: null,
      lines: [],
      containerSize: { width: 0, height: 0 },
      animationFrame: null
    }
  },
  _methods: {
    initLines() {
      this.lines = [];
      const cols = Math.ceil(this.containerSize.width / this.cellSize);
      const rows = Math.ceil(this.containerSize.height / this.cellSize);

      const minHorizontal = Math.max(1, Math.floor(this.lineCount / 2));
      const minVertical = Math.max(1, Math.ceil(this.lineCount / 2));

      for (let i = 0; i < minHorizontal; i++) {
        const fixedPos = Math.floor(Math.random() * rows) * this.cellSize;
        const startPos = Math.random() * this.containerSize.width;

        this.lines.push({
          isHorizontal: true,
          fixedPos,
          position: startPos,
          direction: Math.random() > 0.5 ? 1 : -1,
          length: this.cellSize * (1 + Math.random() * 3),
          speed: 0.5 + Math.random() * 0.5
        });
      }

      for (let i = 0; i < minVertical; i++) {
        const fixedPos = Math.floor(Math.random() * cols) * this.cellSize;
        const startPos = Math.random() * this.containerSize.height;

        this.lines.push({
          isHorizontal: false,
          fixedPos,
          position: startPos,
          direction: Math.random() > 0.5 ? 1 : -1,
          length: this.cellSize * (1 + Math.random() * 3),
          speed: 0.5 + Math.random() * 0.5
        });
      }

      while (this.lines.length < this.lineCount) {
        const isHorizontal = Math.random() > 0.5;
        const fixedPos = Math.floor(Math.random() * (isHorizontal ? rows : cols)) * this.cellSize;
        const startPos = Math.random() * (isHorizontal ? this.containerSize.width : this.containerSize.height);

        this.lines.push({
          isHorizontal,
          fixedPos,
          position: startPos,
          direction: Math.random() > 0.5 ? 1 : -1,
          length: this.cellSize * (1 + Math.random() * 3),
          speed: 0.5 + Math.random() * 0.5
        });
      }
    },
    updateLines() {
      this.lines.forEach(line => {
        line.position += line.direction * line.speed * this.speed;

        // Wrap around when going out of bounds
        const maxPos = line.isHorizontal ? this.containerSize.width : this.containerSize.height;
        if (line.position > maxPos + line.length) {
          line.position = -line.length;
        } else if (line.position < -line.length) {
          line.position = maxPos + line.length;
        }
      });
    },
    getLineStyle(line) {
      const style = {
        'background-color': this.lineColor,
        'opacity': '0.8'
      };

      if (line.isHorizontal) {
        // Horizontal line (follows grid row)
        style.left = '0';
        style.top = `${line.fixedPos}px`;
        style.width = '100%';
        style.height = `${this.lineThickness}px`;
        style['mask-image'] = `linear-gradient(to right, 
          transparent 0%, 
          transparent calc(${line.position}px - 1px), 
          black calc(${line.position}px), 
          black calc(${line.position}px + ${line.length}px), 
          transparent calc(${line.position}px + ${line.length}px + 1px), 
          transparent 100%)`;
      } else {
        // Vertical line (follows grid column)
        style.top = '0';
        style.left = `${line.fixedPos}px`;
        style.height = '100%';
        style.width = `${this.lineThickness}px`;
        style['mask-image'] = `linear-gradient(to bottom, 
          transparent 0%, 
          transparent calc(${line.position}px - 1px), 
          black calc(${line.position}px), 
          black calc(${line.position}px + ${line.length}px), 
          transparent calc(${line.position}px + ${line.length}px + 1px), 
          transparent 100%)`;
      }

      return style;
    },
    updateSize() {
      if (this.container) {
        this.containerSize = {
          width: this.container.offsetWidth,
          height: this.container.offsetHeight
        };
        this.initLines();
      }
    },
    animate() {
      this.updateLines();
      this.animationFrame = requestAnimationFrame(this.animate);
    }
  },
  get methods() {
    return this._methods;
  },
  set methods(value) {
    this._methods = value;
  },
  mounted() {
    this.container = this.$refs.container;
    this.updateSize();
    this.animate();
    window.addEventListener('resize', this.updateSize);
  },
  beforeUnmount() {
    cancelAnimationFrame(this.animationFrame);
    window.removeEventListener('resize', this.updateSize);
  }
}
</script>

<style scoped>
.grid-background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: #1a1a1a;
  background-image: 
    linear-gradient(#2a2a2a 1px, transparent 1px),
    linear-gradient(90deg, #2a2a2a 1px, transparent 1px);
  background-size: v-bind('cellSize + "px " + cellSize + "px"');
  z-index: -1;
}

.grid-line {
  position: absolute;
  background: v-bind(lineColor);
  will-change: transform;
  mask-repeat: no-repeat;
}
</style>