<template>
    <view class="veo-canvas-color-change">
        <canvas style="width: 300px; height: 300px;" canvas-id="lavContainer" id="lavContainer" @click="onClick"
            @touchend="touchend"></canvas>
    </view>
</template>

<script>
    export default {
        name: "veo-canvas-color-change",
        props: {
            img: {
                type: String,
                default: ''
            },
            // 尺寸(宽度)
            width: {
                type: [Number, String],
                default: 300
            },
            // 尺寸(高度)
            height: {
                type: [Number, String],
                default: 300
            }
        },
        computed: {
            options() {}
        },
        data() {
            return {
                clickColor: null,
                canvas: null,
                canvasImageData: null,
                style: {
                    width: this.width ? `${this.width}px` : '100%',
                    height: this.height ? `${this.height}px` : '100%',
                    overflow: 'hidden'
                }
            }
        },
        mounted() {
            this.init()
        },
        methods: {
            init() {
                this.canvas = uni.createCanvasContext('lavContainer')
                this.canvas.drawImage('../../static/logo.png',0,0,300,300)
                // this.canvas.drawImage('../../static/mn.jpg',0,0,300,300)
                // this.canvas.drawImage('../../static/cs.jpg', 0, 0, 300, 300)
                this.canvas.draw()

                // this.canvas.setFillStyle('blue')
                // this.canvas.fillRect(0, 0, 300, 300)
                // this.canvas.draw()

                setTimeout(() => {
                    this.getColorData()
                }, 10)

            },
            getColorData() {
                uni.canvasGetImageData({
                    canvasId: 'lavContainer',
                    x: 0,
                    y: 0,
                    width: this.width,
                    height: this.height,
                    success: (res) => {
                        // console.log(res)
                        this.canvasImageData = res.data
                    }
                }, this)
            },
            /**
             * canvas的点击事件
             * @param {Object} e
             */
            onClick(e) {
                // this.$emit('click')
                const canvas_x = e.detail.x - 15
                const canvas_y = e.detail.y - 15
                this.clickColor = this.getColor(canvas_x, canvas_y)

                this.changeColor(e.detail.x - 15, e.detail.y - 15, this.clickColor, [0, 255, 0, 255])
                // const data = new Uint8ClampedArray([255, 0, 0, 255])
                uni.canvasPutImageData({
                    canvasId: 'lavContainer',
                    x: 0,
                    y: 0,
                    width: this.width,
                    height: this.height,
                    data: this.canvasImageData,
                    success: (res) => {
                        this.getColorData()
                    }
                }, this)

            },
            /**
             * 执行修改颜色
             * @param {Object} x
             * @param {Object} y
             * @param {Object} click_color
             * @param {Object} change_color
             */
            changeColor(x, y, click_color, change_color) {
                const stack = [{
                    x: x,
                    y: y
                }];
                const width = this.width;
                const height = this.height;

                while (stack.length > 0) {
                    const {
                        x,
                        y
                    } = stack.pop();
                    if (x < 0 || x >= width || y < 0 || y >= height) continue;
                    const currentColor = this.getColor(x, y);
                    if (this.diffColor(currentColor, click_color) > 100 || this.diffColor(currentColor,
                        change_color) === 0) continue;

                    const i = this.point2Index(x, y);
                    this.canvasImageData.set(change_color, i)

                    stack.push({
                        x: x + 1,
                        y
                    }, {
                        x: x - 1,
                        y
                    }, {
                        x,
                        y: y + 1
                    }, {
                        x,
                        y: y - 1
                    });
                }

            },
            /**
             * 判断两个颜色是否相同
             * @param {Object} color1
             * @param {Object} color2
             */
            diffColor(color1, color2) {
                return Math.abs(color1[0] - color2[0]) +
                    Math.abs(color1[1] - color2[1]) +
                    Math.abs(color1[2] - color2[2]) +
                    Math.abs(color1[3] - color2[3])
            },
            /**
             * 获取坐标位置的像素数组索引
             * @param {Object} x
             * @param {Object} y
             */
            point2Index(x, y) {
                return (y * this.width + x) * 4
            },
            /**
             * 获取坐标位置的像素数组
             * @param {Object} x
             * @param {Object} y
             */
            getColor(x, y) {
                const i = this.point2Index(x, y)
                return [
                    this.canvasImageData[i],
                    this.canvasImageData[i + 1],
                    this.canvasImageData[i + 2],
                    this.canvasImageData[i + 3],
                ]
            },
            touchend() {
                console.log(222)
            },
            play() {
                this.anim.play()
            },
            stop() {
                this.anim.stop()
            }
        }
    }
</script>