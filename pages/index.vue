<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <div class="title title__decoration">品名</div>
        <input v-model="productName" />
        <p>Preview : {{this.productName}}</p>

        <div class="title title__decoration">
          原材料名
          <span class="sub__title__sub">1列に付き22文字まで。</span>
        </div>
        <div class="sub__title">
          1段目
          <span class="sub__title__sub">文字数 {{this.productIngredientsOne.length }}</span>
        </div>
        <input v-model="productIngredientsOne" />
        <p>Preview : {{ this.productIngredientsOne }}</p>

        <div class="sub__title">
          2段目
          <span class="sub__title__sub">文字数 {{this.productIngredientsSecond.length }}</span>
        </div>
        <input v-model="productIngredientsSecond" />
        <p>Preview : {{ this.productIngredientsSecond }}</p>
        <div class="sub__title">
          3段目
          <span class="sub__title__sub">文字数 {{this.productIngredientsThird.length }}</span>
        </div>
        <input v-model="productIngredientsThird" />
        <p>Preview : {{ this.productIngredientsThird }}</p>
        <div class="sub__title">
          4段目
          <span class="sub__title__sub">文字数 {{this.productIngredientsFourth.length }}</span>
        </div>
        <input v-model="productIngredientsFourth" />
        <p>Preview : {{ this.productIngredientsFourth }}</p>
      </div>
      <div class="col-md-6">
        <div class="title title__decoration">保存方法</div>
        <input v-model="productSave" />
        <p>Preview : {{this.productSave}}</p>

        <div class="title title__decoration">賞味期限</div>
        <input v-model="productLimit" />
        <p>Preview : {{this.productLimit}}</p>

        <div class="title title__decoration">製造者</div>
        <div class="sub__title">1段目</div>
        <input v-model="productOwnerOne" />
        <p>Preview : {{this.productOwnerOne}}</p>
        <div class="sub__title">2段目</div>
        <input v-model="productOwnerSecond" />
        <p>Preview : {{this.productOwnerSecond}}</p>

        <div class="mt-5">
          <div class="title text-center">Control Panel</div>
          <div class="control__box mt-2 text-center">
            <button class="btn btn-primary mr-2 ml-2" @click="download">PDF Download</button>
            <button class="btn btn-secondary mr-2 ml-2" @click="draw">Preview</button>
            <button class="btn btn-danger mr-2 ml-2" @click="canvasDelete">Preview Reflesh</button>
          </div>
        </div>
      </div>
    </div>
    <div id="pdf" class="mt-5 mb-5" style="overflow-x: hidden; overflow-y: hidden; height: 600px;">
      <hr />
      <canvas id="label" width="2523px" height="4067px"></canvas>
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
      productIngredientsOne: "",
      productIngredientsSecond: "",
      productIngredientsThird: "",
      productIngredientsFourth: "",
      productSave: "",
      productOwnerOne: "",
      productOwnerSecond: "",
      productLimit: "",
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
      const canvas = document.getElementById("label");
      if (canvas.getContext) {
        let context = canvas.getContext("2d");
        let i, j;
        const width = 620;
        const height = 365;
        for (i = 0; i <= 3; i++) {
          for (j = 0; j <= 10; j++) {
            context.lineWidth = 0.3;
            context.strokeRect(0 + width * i, 0 + height * j, width, height);

            // 左列
            context.font = "bold 18pt 'Yu Mincho'";
            context.fillText("品名", 30 + width * i, 50 + height * j);
            context.beginPath();
            context.moveTo(30 + width * i, 58 + height * j);
            context.lineTo(width - 30 + width * i, 58 + height * j);
            context.closePath();
            context.lineWidth = 0.5;
            context.stroke();

            context.fillText("原材料", 30 + width * i, 90 + height * j);
            context.beginPath();
            context.moveTo(30 + width * i, 200 + height * j);
            context.lineTo(width - 30 + width * i, 200 + height * j);
            context.closePath();
            context.lineWidth = 0.5;
            context.stroke();

            context.fillText("保存方法", 30 + width * i, 232 + height * j);
            context.beginPath();
            context.moveTo(30 + width * i, 245 + height * j);
            context.lineTo(width - 30 + width * i, 245 + height * j);
            context.closePath();
            context.lineWidth = 0.5;
            context.stroke();

            context.fillText("賞味期限", 30 + width * i, 277 + height * j);
            context.beginPath();
            context.moveTo(30 + width * i, 290 + height * j);
            context.lineTo(width - 30 + width * i, 290 + height * j);
            context.closePath();
            context.lineWidth = 0.5;
            context.stroke();

            context.fillText("製造者", 30 + width * i, 322 + height * j);

            // 右列
            context.font = "bold 22pt 'Yu Mincho'";
            context.fillText(
              this.productName,
              160 + width * i,
              50 + height * j
            );
            context.font = "bold 14pt 'Yu Mincho'";
            context.fillText(
              this.productIngredientsOne,
              160 + width * i,
              90 + height * j
            );
            context.fillText(
              this.productIngredientsSecond,
              160 + width * i,
              120 + height * j
            );
            context.fillText(
              this.productIngredientsThird,
              160 + width * i,
              150 + height * j
            );
            context.fillText(
              this.productIngredientsFourth,
              160 + width * i,
              180 + height * j
            );

            context.fillText(
              this.productSave,
              160 + width * i,
              232 + height * j
            );
            context.fillText(
              this.productLimit,
              160 + width * i,
              277 + height * j
            );
            context.fillText(
              this.productOwnerOne,
              160 + width * i,
              322 + height * j
            );
            context.fillText(
              this.productOwnerSecond,
              160 + width * i,
              352 + height * j
            );
          }
        }
      }
    },
    canvasDelete() {
      const canvas = document.getElementById("label");
      if (canvas.getContext) {
        let context = canvas.getContext("2d");
        context.clearRect(0, 0, canvas.width, canvas.height);
      }
    },
    download() {
      const JsPDF = require("jspdf"); // read jspdf module
      require("jspdf-autotable");
      const html2canvas = require("html2canvas");

      let pdf = new JsPDF("portrait", "mm", "a4");

      let canvas = document.getElementById("label");
      let img = canvas.toDataURL("image/png");

      pdf.addImage(img, "png", 5, 5, 205, 289);

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