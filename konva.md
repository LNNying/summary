vue-kanva

安装 npm install vue-konva konva --save
在main.js 中 引入vue-konva

import VueKonva from 'vue-konva'

Vue.use(VueKonva);


网站  https://konvajs.org/docs/shapes/Arrow.html

v-stage  场景   只能有一个

v-layer  层级   v-stage 下有多个

v-shape  图形   v-layer 下有多个

v-group  图形组 v-layer 下有一个  v-group下包含多个图形


基本config配置
v-stage 包含

{
    width, // 宽 number
    height, // 高 number
    draggable, // 是否可拖放
}

shape 图形
  图形基本配置
  {
     strokeWidth, // 线宽 可选 number
     fill, // 填充颜色 可选
     stroke, // 线条颜色 可选
     shadowColor, // 阴影颜色
     shadowOffset, // 阴影偏移量 {x: 0, y: 0} => 默认
     shadowOpacity, // 阴影透明度 0-1
     shadowBlur, // 阴影模糊度 number
     cornerRadius, // 圆角 number 四个角 [0, 10, 0, 10] [左上角，右上角，左下角，右下角]
     opacity, // 透明度 0-1
     visible, // 是否可见 通过 shape.show() layer.draw() -> (图形显示，层级渲染)  shape.hide() layer.draw() -> (图形隐藏，层级渲染)
     draggable, // 是否可拖放
     globalCompositeOperation, // 混合模式操作  值 'xor'
     fillAfterStrokeEnabled, // 是否先绘制线条在填充  默认反过来  也可以 shape.fillAfterStrokeEnabled(true);
  }

  以下为每一个shape配置
    v-rect 矩形
      {
         x, // x坐标  必填 number
         y, // Y坐标 必填 number
         width, // 宽 必填 number
         height, // 高 必填 number
      }

    v-circle 圆形
      {
         x, // x坐标  必填 number
         y, // Y坐标 必填 number
         radius, // 半径 必填 number
      }

    v-ellipse 椭圆
      {
         x, // x坐标  必填 number
         y, // Y坐标 必填 number
         radiusX, // x方向半径 必填 number
         radiusY, // y方法半径 必填 number
      }

    v-wedge 楔形或扇形
      {
         x, // x坐标  必填 number
         y, // Y坐标 必填 number
         radius, // 半径 必填 number
         rotation, // 旋转角度  必填 number  可为负值
      }

    v-line 线条
      {
        points, // 数组 为每个点位的坐标 如 [5, 70, 140, 23, 250, 60, 300, 20],
        lineCap, // 线头 形状  值bevel=>斜面 round=>圆角 miter=>倒角
        lineJoin, // 用于线条连接处 值bevel=>斜面 round=>圆角 miter=>倒角  也有使用方法 .lineJoin()
        dash, // 线形状 如点线  [33, 10] （参1 线段长度  参2 线段间间距） => 为一组  ... 可多组
        closed, // 是否康瓦线 就是可以形成多边形 true  但是点数必须大于等于3个点位
        tension, // 张力形状  就是曲线  取值 0-1
                 // closed 与 tension 一起连用可形成曲性闭合图形
      }

    v-sprite 精灵  见网站

    v-image 图片  见网站

    v-text 文字 对css中文字样式都可直接用
      {
         x: 20,
         y: 60,
         text:"COMPLEX TEXT\n\nAll the world's a stage, and all the men and women merely players. They have their exits and their entrances.",
         fontSize: 18,
         fontFamily: 'Calibri',
         fill: '#555',
         width: 300,
         padding: 20,
         align: 'center',
      }


认知：
在vue中通过this.$refs.[]获取到的是stage在vue中的虚拟dom  通过this.$refs.[].getNode().getStage()才能获取到stage本身
在拖拽整体画布(或某个图形)的时候会自动修改画布中x,y 获取方式 this.$refs[].getNode().getStage().attrs.x/y  attrs中存放的是画布的属性 如 x,y,offsetX,offsetY,width,height等
stage中也有scale,rotation,offsetX/Y等;
画布在旋旋转的时候是以左上角为基点，通过offset:{x,y}调整偏移量. 相当于canvas中通过translateX/Y调整坐标系一样
stage.getPointerPosition()获取的是鼠标在画布中坐标

.batchDraw() 重新绘制   如果图形没有变化 通过.draw() 重新绘制


