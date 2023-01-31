<template>
  <div id="container" >
    <div id="content">
      <header>
        <h3>신상품</h3>
        <p>새로운 상품을 만나보세요</p>
      </header>
      <main :style="colChanged">
        <div id="product" v-for="product in products" :key="product.id">
          <img :src="product.img"/>
          <p :style="brandChanged">{{ product.brand }}</p>
          <h3 :style="titleChanged">{{ product.title }}</h3>
          <span :style="memoChanged">{{ product.memo }}</span>
          <span :style="priceChanged">{{ product.price }}</span>
          <span :style="discountChanged">{{ product.discount }}</span>
          <span :style="originalPriceChanged">{{ product.originalPrice }}</span>
        </div>
      </main>
    </div>
    <div>
      <div id="control">
        <form>
          <h4 style="display:inline; margin-right: 22px">컬럼수</h4>
          <input type="number" v-model="col"/>
        </form>
        <form>
          <h4>브랜드명</h4>
          <div>
            글씨색상
            <input type="text" v-model="designs.brand.color"/>
          </div>
          <div>
            글씨크기
            <input type="text" v-model="designs.brand.fontSize"/>
          </div>
        </form>
        <form>
          <h4>상품명</h4>
          <div>
            글씨색상
            <input type="text" v-model="designs.title.color"/>
          </div>
          <div>
            글씨크기
            <input type="text" v-model="designs.title.fontSize"/>
          </div>
        </form>
        <form>
          <h4>설명</h4>
          <div>
            글씨색상
            <input type="text" v-model="designs.memo.color"/>
          </div>
          <div>
            글씨크기
            <input type="text" v-model="designs.memo.fontSize"/>
          </div>
        </form>
        <form>
          <h4>판매금액</h4>
          <div>
            글씨색상
            <input type="text" v-model="designs.price.color"/>
          </div>
          <div>
            글씨크기
            <input type="text" v-model="designs.price.fontSize"/>
          </div>
        </form>
        <form>
          <h4>할인금액</h4>
          <div>
            글씨색상
            <input type="text" v-model="designs.discount.color"/>
          </div>
          <div>
            글씨크기
            <input type="text" v-model="designs.discount.fontSize"/>
          </div>
        </form>
        <form>
          <h4>원가</h4>
          <div>
            글씨색상
            <input type="text" v-model="designs.originalPrice.color"/>
          </div>
          <div>
            글씨크기
            <input type="text" v-model="designs.originalPrice.fontSize"/>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      col: 4,
      designs: {
        brand:{
          color: '#000',
          fontSize: '10',
        },
        title:{
          color: '#000',
          fontSize: '15',
        },
        memo:{
          color: '#000',
          fontSize: '10',
        },
        price:{
          color: '#000',
          fontSize: '20',
        },
        discount:{
          color: '#ff0000',
          fontSize: '15',
        },
        originalPrice:{
          color: '#999',
          fontSize: '13',
        },
      },
      products: [
        {
          id: 1,
          img: '../src/assets/1.png',
          brand:'샘표',
          title:'진간장 금S 1.8L',
          memo:'언제나 함깨해 온 그 맛',
          price:'4,500원',
          discount:'-3,650원',
          originalPrice:'8,150원'
        },
        {
          id: 2,
          img:'../src/assets/2.jpg',
          brand:'동서식품',
          title:'[맥심]모카 골드 250T',
          memo:'커피 한 잔의 여유',
          price:'27,900원',
          discount:'-3,600원',
          originalPrice:'31,150원'
        },
        {
          id: 3,
          img:'../src/assets/3.jpg',
          brand:'동원',
          title:'딤섬 부추 창편 390g X 2개입',
          memo:'소스와 함께먹는 부드러움',
          price:'6,980원',
          discount:'-2,000원',
          originalPrice:'8,980원'
        },
        {
          id: 4,
          img:'../src/assets/4.jpg',
          brand:'동원',
          title:'딤섬 샤오롱바오 390g X 2개입',
          memo:'고소한 육즙 가득',
          price:'6,980원',
          discount:'-2,000원',
          originalPrice:'8,980원'
        },
      ],
      controls: [
        {
          id: 1,
          title: '브랜드명',
          name: 'brand'
        },
        {
          id: 2,
          title: '상품명',
          // color: this.designs.title.color,
          // size: this.designs.title.fontSize
        },
        {
          id: 3,
          title: '설명',
          // color: this.designs.memo.color,
          // size: this.designs.memo.fontSize
        },
      ]
    }
  },
  computed: {
    colChanged() {
      return {
        'display': 'grid',
        'gridTemplateColumns': `repeat(${this.col}, 1fr)`,
      }
    },
    brandChanged() {
      return {
        'color': this.designs.brand.color,
        'fontSize': this.designs.brand.fontSize +'px',
        'margin': '1px'
      }
    },
    titleChanged() {
      return {
        'color': this.designs.title.color,
        'fontSize': this.designs.title.fontSize +'px',
        'margin': '1px'
      }
    },
    memoChanged() {
      return {
        'color': this.designs.memo.color,
        'fontSize': this.designs.memo.fontSize +'px',
        'display': 'block'
      }
    },
    priceChanged() {
      return {
        'color': this.designs.price.color,
        'fontSize': this.designs.price.fontSize +'px',
        'marginRight': '5px',
        'fontWeight': 'bold'
      }
    },
    discountChanged() {
      return {
        'color': this.designs.discount.color,
        'fontSize': this.designs.discount.fontSize +'px',
        'display': 'inline',
        'fontWeight': 'bold'
      }
    },
    originalPriceChanged() {
      return {
        'color': this.designs.originalPrice.color,
        'fontSize': this.designs.originalPrice.fontSize +'px',
        'display':'block',
        'textDecoration': 'line-through'
      }
    },
  }
}
</script>

<style>
  #container{
    display: flex;
    background-color: #ccc;
  }

  #content{
    margin:10px;
  }

  header {
    margin: 50px;
    text-align: center;
  }
  header > h3 {
    margin: 0px
  }
  header > p {
    margin: 0px
  }

  #content {
    background-color: #fff;
  }

  #product {
    margin: 10px;
  }
  #product > p {
    margin-top: 5px;
    margin-bottom: 2px;
  }

  main {
    margin: 20px;
  }

  img {
    width:100%;
    height: 300px;
  }

  #control {
    background-color:#fff;
    margin: 10px;
    padding-top: 20px;
    padding-bottom: 20px;
  }
  #control > form {
    margin: 15px
  }
  #control > form > h4 {
    margin-bottom: 10px
  }

</style>