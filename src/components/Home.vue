<template>
  <div class="slides">
    <b-carousel
      id="carousel-1"
      v-model="slide"
      :interval="3000"
      controls
      indicators
      background="#ccc"
      img-width="1024"
      img-height="480"
      style="text-shadow: 1px 1px 2px #000;"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd"
    >
      <b-carousel-slide img-src="https://storage-asset.msi.com/global/picture/banner/banner_16206346080811b46b44b65364efbf6898a5b9cbc5.jpeg" ></b-carousel-slide>

      <b-carousel-slide img-src="https://storage-asset.msi.com/global/picture/banner/banner_1620635919f28c2997eeedd568b072ea04ca5a67c1.jpeg" ></b-carousel-slide>

      <b-carousel-slide img-src="https://storage-asset.msi.com/global/picture/banner/banner_16206352348866ed42a0c153cf608565d872e4765e.jpeg" ></b-carousel-slide>

      <b-carousel-slide img-src="https://storage-asset.msi.com/global/picture/banner/banner_1620637220ba7bd83b787a67761ef60081d80bee56.jpeg" ></b-carousel-slide>

    </b-carousel>
<br>
  


    <b-container class="bv-example-row" >
                <b-row>
                    <b-col v-for="product in productfields" v-bind:key="product._id" class="col-xl-4 col-lg-4 col-md-6 col-sm-12 ">
                    <b-col class="single-new-pro mb-30 text-center">
                      <b-col class="product-img">
                        <img :src="`http://localhost:5000/images/${product.image}`" class="imagediv">
                      </b-col>
                        <b-row class="product-caption">
                                <h5 class="titulli">{{ product.name }}</h5>
                                <p class="price">{{product.price}}.00 <span class="euro">Euro</span> </p>
                            
                            <b-col class="pb-3">
                                
                                    <!-- v-on:click="addToCart" -->
                                <b-button  class="btn-danger">
                               <!-- <b-button v-b-modal.modal-1> -->
                                 Add to Cart</b-button>

                            
                            </b-col>
                        </b-row>
                    </b-col>
                    </b-col>
                </b-row>
            </b-container>
              
  </div>
</template>


<script>
/* eslint-disable */
import axios from 'axios'
  export default {
    data() {
      return {
        slide: 0,
        sliding: null,
        productfields:{},
        products: {},
      }
    },
    created () {
    axios.get(`http://localhost:4000/products`)
    .then(response => {
      this.productfields = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  },
    methods: {
      onSlideStart() {
        this.sliding = true
      },
      onSlideEnd() {
        this.sliding = false
      },
      onSubmit (evt) {
      evt.preventDefault()
      axios.post(`http://localhost:4000/products`, this.products)
      .then(function (response) {
        console.log(response);
        })
      
    }
  }
  }


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@media (max-width: 575.98px) {
  .bv-example-row {
     display: block;
  width: 280px;
  height: auto;
  padding: 5px;
  }
}

.product-img{
  border: 1px solid lightgrey;
  padding: 7px;

  background-color: white;
  border-radius: 3%;
}
.titulli{
  color: #C60021;
  font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  font-weight: bold;
  font-size: 1.5rem;
}
.price{
  color: black;
  font-size: 1.2rem;
}
.euro{
  font-size: 1rem;
  color: gray;
}
.single-new-pro .product-img {
    overflow: hidden;
    margin-bottom: 15px
}

.single-new-pro .product-img img {
    width: 100%;
    transform: scale(1);
    -webkit-transition: all .4s ease-out 0s;
    -moz-transition: all .4s ease-out 0s;
    -ms-transition: all .4s ease-out 0s;
    -o-transition: all .4s ease-out 0s;
    transition: all .4s ease-out 0s
}
.single-product .product-img {
    position: relative;
    overflow: hidden
}

.text-center{text-align:center!important}
</style>
