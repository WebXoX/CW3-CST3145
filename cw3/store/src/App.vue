<template>
<div class="main-wrapper">
  <div id="app">
    <nav class="nav">
        <div class="logo">
                <img class="logoH" height="100px" src="gr.png">
            </div>
            <div class="Courses">
            <h1 @click='showLessons=true'>Courses</h1>
            </div>
    
        <div class="checkOut">
            <button class="checkB" @click='showCheckOut' v-bind:disabled="!cartLength">
                {{cartLength}}
                <span id="cart" class="fas fa-cart-plus"></span> 
            </button>
        </div>
    </nav>
    <div class="page" v-if="showLessons===true">
        <product-list  @addProduct="addItem" :products="products" :cart="cart"></product-list>
    </div>
  <div class="carPage" v-else>  
    <checkout @removeCart="removeCart"  :products="products" :cart="cart"></checkout>
  </div>
  </div>
  <div class="footer">
         <p>
            @Joe Shaju Perinchery
         </p>
    </div>
  </div>
</template>

<script>
import productList from "./components/ProductList.vue";
import checkout from "./components/FormCheckout.vue";
export default {
  name: 'App',
  components: {productList,checkout },
  data(){
    return {
      sitename: 'Available Courses',
      showLessons: true,
      products: [],
      cart: []
    }
  },
  methods: {  //methods
            /*Method to add items to cart*/
            addItem(product){   
                if(product.quantity>0)
                {
                    product.quantity-=1 ;
                    this.cart.push( product);
                }
            },
            /*Method to switch between pages*/
            showCheckOut(){
                this.showLessons = this.showLessons ?false:true;
            },
            /*finds product that is similar*/  
             productFinder(id) {
               for (let i =0; i< this.products.length;i++)
               {
                if(this.products[i].id===id)
                    return this.products[i];
               }
             },
            /*Method to remove from cart and add back to product*/  
             removeCart(id){
              
                for(let i =0;i<this.cart.length;i++)
                    {
                        if(id===this.cart[i])
                        {
                            this.cart.splice(i,1);
                            this.productFinder(id.id).quantity+=1;
                            break;
                        }
                    }
             },
             put(json){
                this.products=json;
             }
        },
        /*computed is for calculating values*/ 
        computed: {
            /*returns length of cart*/ 
            cartLength: function() {
                return this.cart.length || '';
            }
        },
        created: function () {
            console.log('requesting data from the server ...')
            // retrieving data from the server
            const store = this;
            fetch('http://localhost:3000/collection/lessons').then(
                function (response) {
                    response.json().then(
                        function (json) {
                            // storing the response
                            store.products = json;
                        });
                }
            )
        }}




</script>


