<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <div class="title title__decoration">品名</div>
        <input v-model="productName" />
        <p>Preview : {{ this.productName }}</p>

        <div class="title title__decoration">原材料名</div>
        <div class="sub__title">
          <span class="sub__title__sub"
            >文字数 {{ this.productIngredients.length }}</span
          >
        </div>
        <input v-model="productIngredients" />
        <p>Preview : {{ this.productIngredients }}</p>
      </div>
      <div class="col-md-6">
        <div class="title title__decoration">内容量</div>
        <input v-model="productContent" />
        <p>Preview : {{ this.productContent }}</p>
        <!-- <div class="title title__decoration">賞味期限</div>
        <input v-model="productLimit" />
        <p>Preview : {{ this.productLimit }}</p> -->

        <div class="title title__decoration">保存方法</div>
        <input v-model="productSave" />
        <p>Preview : {{ this.productSave }}</p>
        <div class="title title__decoration">製造者</div>
        <div class="sub__title">1段目</div>
        <input v-model="productOwnerOne" />
        <p>Preview : {{ this.productOwnerOne }}</p>
        <div class="sub__title">2段目</div>
        <input v-model="productOwnerSecond" />
        <p>Preview : {{ this.productOwnerSecond }}</p>
        <div class="sub__title">3段目</div>
        <input v-model="productOwnerThird" />
        <p>Preview : {{ this.productOwnerThird }}</p>

        <div class="mt-5">
          <div class="title text-center">Control Panel</div>
          <div class="control__box mt-2 text-center">
            <button class="btn btn-primary mr-2 ml-2 mt-2" @click="download">
              PDF Download
            </button>
            <button class="btn btn-secondary mr-2 ml-2 mt-2" @click="draw">
              Preview
            </button>
            <button class="btn btn-danger mr-2 ml-2 mt-2" @click="canvasDelete">
              Preview Reflesh
            </button>
          </div>
        </div>
      </div>
    </div>
    <div
      id="pdf"
      class="mt-5 mb-5"
      style="overflow-x: hidden; overflow-y: hidden; height: 900px"
    >
      <hr />
      <canvas id="label_vertical" width="3578.7px" height="2551.2 px"></canvas>
    </div>
  </div>
</template>

<script>
// pdfmakeはできる幅が狭く、デザインが必要とされるレイアウトは厳しかった。
// import pdfMake from "pdfmake/build/pdfmake";
// import pdfFonts from "pdfmake/build/vfs_fonts";
// pdfMake.vfs = pdfFonts.pdfMake.vfs; // pdfMakeを読み込んだあとにpdfFontsを読み込む必要があるため、この宣言がないとエラーが起きる。

//How to use jspdf in Nuxt   https://forum.vuejs.org/t/how-to-use-jspdf-in-nuxt/52323/2
// import JsPDF from "jspdf";

export default {
  data() {
    return {
      productName: "",
      productIngredients: "",
      productSave: "",
      productOwnerOne: "",
      productOwnerSecond: "",
      productOwnerThird: "",
      productLimit: "",
      productContent: "",
    };
  },

  computed: {
    stringCounter(text) {
      return text.length;
    },
  },

  // 参考　https://www.it-swarm.dev/ja/javascript/html-canvas%E3%82%92gifjpgpngpdf%E3%81%A8%E3%81%97%E3%81%A6%E3%82%AD%E
  // 3%83%A3%E3%83%97%E3%83%81%E3%83%A3%E3%81%97%E3%81%BE%E3%81%99%E3%81%8B%EF%BC%9F/957622337/
  methods: {
    draw() {
      const canvas = document.getElementById("label_vertical");
      if (canvas.getContext) {
        let context = canvas.getContext("2d");
        let i, j;
        const width = 501;
        const height = 826;
        for (i = 0; i <= 6; i++) {
          for (j = 0; j <= 2; j++) {
            context.lineWidth = 0.3;
            context.strokeRect(0 + width * i, 0 + height * j, width, height);

            // 左列
            context.font = "bold 18pt 'Yu Mincho'";
            context.fillText("品名", 32.7 + width * i, 62.2 + height * j);
            context.beginPath();
            context.moveTo(32.7 + width * i, 72.7 + height * j);
            context.lineTo(width - 32.7 + width * i, 72.7 + height * j);
            context.closePath();
            context.lineWidth = 0.5;
            context.stroke();

            context.fillText("原材料", 32.7 + width * i, 102.1 + height * j);
            context.beginPath();
            context.moveTo(32.7 + width * i, 497.1 + height * j);
            context.lineTo(width - 32.7 + width * i, 497.1 + height * j);
            context.closePath();
            context.lineWidth = 0.5;
            context.stroke();

            context.fillText("内容量", 32.7 + width * i, 522.1 + height * j);
            context.beginPath();
            context.moveTo(32.7 + width * i, 532.1 + height * j);
            context.lineTo(width - 32.7 + width * i, 532.1 + height * j);
            context.closePath();
            context.lineWidth = 0.5;
            context.stroke();

            context.fillText("賞味期限", 32.7 + width * i, 560.3 + height * j);
            context.beginPath();
            context.moveTo(32.7 + width * i, 570.3 + height * j);
            context.lineTo(width - 32.7 + width * i, 570.3 + height * j);
            context.closePath();
            context.lineWidth = 0.5;
            context.stroke();

            context.fillText("保存方法", 32.7 + width * i, 600.3 + height * j);
            context.beginPath();
            context.moveTo(32.7 + width * i, 678.1 + height * j);
            context.lineTo(width - 32.7 + width * i, 678.1 + height * j);
            context.closePath();
            context.lineWidth = 0.5;
            context.stroke();

            context.fillText("製造者", 32.7 + width * i, 708.1 + height * j);

            // 右列
            context.font = "bold 20pt 'Yu Mincho'";
            context.fillText(
              this.productName,
              148.2 + width * i,
              62.2 + height * j
            );

            // 原材料名を15文字毎に分割し配列に格納する。
            let productIngredientsTexts = [];
            console.log(this.productIngredients);
            const textLength = this.productIngredients.length;
            for (let k = 0; k < textLength; k += 15) {
              productIngredientsTexts.push(
                this.productIngredients.slice(k, k + 15)
              );
            }

            // テキストを描画
            context.font = "bold 16pt 'Yu Mincho'";
            for (let k = 0; k < productIngredientsTexts.length; k += 1) {
              context.fillText(
                productIngredientsTexts[k],
                148.2 + width * i,
                102.1 + k * 35 + height * j
              );
            }

            // 内容量
            context.fillText(
              this.productContent,
              148.2 + width * i,
              522.1 + height * j
            );

            // 保存方法
            let productSaveTexts = [];
            for (let k = 0; k < this.productSave.length; k += 17) {
              productSaveTexts.push(this.productSave.slice(k, k + 17));
            }
            // テキストを描画
            context.font = "bold 14pt 'Yu Mincho'";
            for (let k = 0; k < productSaveTexts.length; k += 1) {
              context.fillText(
                productSaveTexts[k],
                148.2 + width * i,
                600.3 + k * 30 + height * j
              );
            }

            context.font = "bold 16px 'Yu Mincho'";
            // 賞味期限
            context.fillText(
              this.productLimit,
              148.2 + width * i,
              560.3 + height * j
            );

            // 製造者
            context.fillText(
              this.productOwnerOne,
              148.2 + width * i,
              708.1 + height * j
            );
            context.fillText(
              this.productOwnerSecond,
              148.2 + width * i,
              733.1 + height * j
            );
            context.fillText(
              this.productOwnerThird,
              148.2 + width * i,
              758.1 + height * j
            );
          }
        }
      }
    },
    canvasDelete() {
      const canvas = document.getElementById("label_vertical");
      if (canvas.getContext) {
        let context = canvas.getContext("2d");
        context.clearRect(0, 0, canvas.width, canvas.height);
      }
    },
    download() {
      const JsPDF = require("jspdf"); // read jspdf module
      require("jspdf-autotable");
      const html2canvas = require("html2canvas");

      let pdf = new JsPDF("landscape", "mm", "a4");

      let canvas = document.getElementById("label_vertical");
      let img = canvas.toDataURL("image/png");

      pdf.addImage(img, "png", 6, 6, 291, 205);

      window.html2canvas = html2canvas;
      pdf.save("food_label.pdf");
    },
  },
};
</script>

<style scoped>
.title {
  font-size: 24px;
}
.sub__title {
  font-size: 20px;
}

.sub__title__sub {
  font-size: 14px;
  color: #646464;
}

.title__decoration {
  border-bottom: solid 1px #c0c0c0;
  margin-bottom: 20px;
  margin-top: 50px;
}

.control__box {
  border: solid 1px #c0c0c0;
  border-radius: 20px;
  padding: 50px 30px;
}
</style>