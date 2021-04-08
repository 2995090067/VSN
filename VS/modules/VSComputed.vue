<template>
  <div>
    <verification-code.vue>
      <VSModules id="nav"></VSModules>
    </verification-code.vue>
  </div>
</template>

<script>
  import VerificationCode from "./VerificationCode";
  import VSModules from "./VSModules";

  export default {
    name: "VSComputed",
    components: {
      VerificationCode,
      VSModules
    },
    created() {
      // 创建画板
      let canvas = document.getElementById("nav")
      //2d画笔
      let context = canvas.getContext("2d");
      canvas.onclick = function () {
        context.clearRect('0', '0', '120', '40');
        // 重新绘画
        draw();
      }
    },
    methods: {
      draw() {
        // 背景大小 0，0，120,40
        context.strokeRect(0, 0, 120, 40);
        //验证码
        let NCode = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k"];
        // rbg三原色
        function getColor() {
          let r = Math.floor(Math.random() * 256);
          let g = Math.floor(Math.random() * 256);
          let b = Math.floor(Math.random() * 256);
          //抛出随机的三原色字符串
          return "rgb(" + r + "," + g + "," + b + ")";
        }

        for (let i = 0; i < 4; i++) {
          //x轴和y轴坐标
          let x, y;
          x = 20 + 20 * i;
          y = 20 + 10 * Math.random();//随机数
          // 获取数组下标所代表的内容
          let index = Math.floor(Math.random() * NCode.length);
          // console.log(index+"获取数组下标")
          let htmltext = NCode[index];
          // 随机数,5以上大写
          let MAXS = Math.random() * 10 + 1;
          //判断是否数字
          if (isNaN(htmltext)) {
            if (MAXS > 5) {
              // 强转大小写
              // console.log(htmltext+"强转了");
              var a = htmltext.toUpperCase();
              ioop(a);
            } else {
              //没强转
              // console.log("没强转呢！===》"+htmltext)
              ioop(htmltext);
            }
          } else {
            // console.log("是数字"+htmltext);
            ioop(htmltext);
          }
          line();//控制线
          dribs();//控制点
          // 控制随机线的数量颜色
          function line() {
            for (let i = 0; i <= 1; i++) {
              //验证码上显示线条
              context.strokeStyle = getColor();
              context.beginPath();
              context.moveTo(Math.random() * 120, Math.random() * 40);
              context.lineTo(Math.random() * 120, Math.random() * 40);
              context.stroke();
            }
          }

          //控制随机点的颜色数量
          function dribs() {
            for (let i = 0; i <= 1; i++) {
              //验证码上显示小点
              context.strokeStyle = getColor();
              context.beginPath();
              let x = Math.random() * 120;
              let y = Math.random() * 40;
              context.moveTo(x, y);
              context.lineTo(x + 1, y + 1);
              context.stroke();
            }
          }

          //样式属性
          function ioop(a) {
            //控制角度
            // 控制canvas的定位，控制画布的旋转实现字体的假旋转
            context.translate(x, y);
            // alert(x)
            // alert(y)
            let deg = Math.random() * 90 * Math.PI / 180;
            context.rotate(deg)
            //字体样式
            context.font = 'blod 20px 微软雅黑';
            // 填写随机内容循环四次
            context.fillText(a, 0, 0);
            // 控制三原色
            var Color = getColor();
            //赋予随机三原色
            context.fillStyle = getColor();
            //随机旋转后复位再次旋转
            context.rotate(-deg)
            // alert(-deg)
            context.translate(-x, -y)
          }
        }
      }
    },

  }
</script>

<style scoped>

</style>