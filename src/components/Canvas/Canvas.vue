<template>
    <div class="canvasContainer">
        <canvas ref="painting" id="canvas"
                width="490"
                height="220"
                @touchstart="onTouchStart"
                @touchend="onTouched"
                @touchmove="onTouchMove"
                @mousedown="onMouseDown"
                @mousemove="onMouseMove"
                @mouseup="onMouseUp"
                @mouseleave="onMouseUp"
        ></canvas>

    </div>
</template>

<script>

  export default {
    props: {
      currentColor: {
        type: String,
        default: '#000',
      },
      availableColors: {
        type: Array,
        required: true
      }
    },
    data() {
      return {
        context: null,
        canvas: null,
        paint: false,
        dragable: [],
        mouseEvent: null,
        touch: null,
        mousePos: { x: 0, y: 0 },
        lastPos: this.mousePos,
        storeMouseX: [],
        storeMouseY: [],
        storeColors: [],
        colors: [],
      }
    },
    mounted() {
      this.canvas = document.getElementById('canvas');
      this.context = this.canvas.getContext('2d');
      this.colors = this.availableColors;
    },
    computed: {
      curColor: function () {
        return this.currentColor
      }
    },
    methods: {
      onMouseUp() {
        this.paint = false;
      },
      onMouseDown(e) {
        this.paint = true;
        this.lastPos = this.getMousePos(canvas, e);
        this.storeMouseValues(this.lastPos.x, this.lastPos.y);
        this.redraw();
      },
      onMouseMove(e) {
        if (this.paint) {
          this.mousePos = this.getMousePos(canvas, e);
          this.storeMouseValues(this.mousePos.x, this.mousePos.y, this.paint);
          this.redraw();
        }
      },
      storeMouseValues(x, y, ableToPaint) {
        this.storeMouseX.push(x);
        this.storeMouseY.push(y);
        this.dragable.push(ableToPaint);
        this.storeColors.push(this.curColor);
      },
      redraw() {
        this.context.clearRect(0, 0, this.context.canvas.width, this.context.canvas.height); // Clears the canvas
        this.context.lineJoin = "round";
        this.context.lineWidth = 5;

        for (let i = 0; i < this.storeMouseX.length; i++) {
          this.context.beginPath();

          if (this.dragable[i] && i) {
            this.context.moveTo(this.storeMouseX[i - 1], this.storeMouseY[i - 1]);
          } else {
            this.context.moveTo(this.storeMouseX[i] - 1, this.storeMouseY[i]);
          }

          this.context.strokeStyle = this.storeColors[i];
          this.context.lineTo(this.storeMouseX[i], this.storeMouseY[i]);
          this.context.closePath();
          this.context.stroke();
        }
      },
      getMousePos(canvasDom, mouseEvent) {
        const rect = canvasDom.getBoundingClientRect();
        return {
          x: mouseEvent.offsetX,
          y: mouseEvent.offsetY
        };
      },

      /**
       * Clear the CANVAS
       */
      clearCanvas() {
        console.log(canvas);
//        canvas.width = canvas.width;
      },
      /**
       * Methods for TOUCH EVENTS
       * onTouchStart:
       * onTouched:
       * onTouchMove:
       * getTouchPosition:
       */
      onTouchStart(e) {
        this.mousePos = this.getTouchPosition(canvas, e);
        this.touch = e.touches[0];
        console.log(this.touch);
        this.mouseEvent = new MouseEvent('mousedown', {
          clientX: this.touch.clientX,
          clientY: this.touch.clientY
        });
        canvas.dispatchEvent(this.mouseEvent);
      },
      onTouched(e) {
        console.log('mvoee', canvas);
        this.mouseEvent = new MouseEvent('mouseup', {});
        canvas.dispatchEvent(this.mouseEvent);
      },
      onTouchMove(e) {
        this.touch = e.touches[0];
        this.mouseEvent = new MouseEvent('mousemove', {
          clientX: this.touch.clientX,
          clientY: this.touch.clientY
        });
        console.log(this.mouseEvent);
        console.log(canvas);
        canvas.dispatchEvent(this.mouseEvent);
      },
      getTouchPosition(canvasDom, touchEvent) {
        console.log(canvasDom, touchEvent);
        return {
          x: touchEvent.touches[0].clientX,
          y: touchEvent.touches[0].clientY
        };
      },
    }
  }

</script>

<style>
    .canvasContainer {
        width: 100%;
        height: 85vh;
        border-radius: 15px;
        background-color: white;
        box-shadow: 1px 3px 4px 1px #00000030;
        text-align: center;
    }

    #canvas {
        box-shadow: 0 1px 1px #00000014;
    }
</style>
