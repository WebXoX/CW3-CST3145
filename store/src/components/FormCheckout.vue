<template>

        <div class="cartWrapper">
            <h2 class="cartHead">CART</h2>
            <div class="cartItem"  >
                <div class="filledCart" v-if="cartLength>0">
                    <div class="productss"  >
                        <div class="cartProduct" v-for="(items,index) in removeDuplicates(cart)" :key="index" v-if="cartCounting(items)" > 
                            <figure>
                            <img height="200px" width="180px" v-bind:src="productFinder(items.id).image">
                            </figure>
                            <!-- CART CONTENT -->
                            <div id="content">
                                <p >Subject: <b>{{productFinder(items.id).title}}</b></p>
                                <p> City: <b>{{productFinder(items.id).location}}</b></p>
                                <p>Price: <b>{{productFinder(items.id).price}}</b></p>
                                <p>amount: <b>{{cartCounting(items)}}</b></p>
                                <div>
                                    <span v-for="n in (items).rating" :key="n"><i class="fa-solid fa-star"></i></span>
                                    <span v-for="n in 5-(items).rating" :key="n+1"><i class="fa-regular fa-star"></i></span>
             
                                </div>
                                <button id="rButton" @click="removeCart(items)">remove</button>
                               
                            </div>
                        </div>
                    </div>
                    <div class="order">
                        <h2>Checkout</h2>
                        <p id="fName">
                            <strong>First Name:</strong>
                            <!-- linking feilds to data-->
                            <input type="letters" v-model.trim="order.firstName"/>
                        </p>
                        <p id="lName">
                            <strong>Last Name:</strong>
                            <!-- linking feilds to data-->
                            <input type="letters" v-model.trim="order.lastName"/>
                        </p>
                        <p id="number">
                            <strong>Phone Number:</strong> 
                            <input   type="number" maxlength="10" v-model="order.number"/>
                        </p>
                        <button id="submitB" @click="submitForm" v-bind:disabled="!canForm" >Place Order</button>
                    </div>

                </div>
                <!-- if cart is empty -->
                <div class="empty" v-else>
                    
                        <b id="bold1">Orders</b>
                        <p id="notBold">You have no orders yet.</p>
                    
                </div>
            </div>
        </div>
    <!-- </div> -->
</template>
<script>
export default{
    name:"FormCheckout",
    props:{ products:{type: Array, required: true},cart:{type: Array, required: true}},
    data(){
        return{
            order:{
                firstName: " ",
                lastName:' ',
                address:'',
                city:'',
                state: '',
                zip:'',
                gift:'',
                sendGift:'Send as a Gift',
                dontSendGift:'Do not send as a Gift',
                method:'home',
                rating: 3
            }
        }; },
    methods: {
        removeCart(id){
        this.$emit('removeCart',id);
      },
        removeDuplicates(cart){
        // this.$emit('removeDuplicates',cart);
        var unique = [];
                cart.forEach(element => {
                    if (!unique.includes(element)) {
                        unique.push(element);
                    }
                });
                return unique;
      }, cartCounting(id){
        let count = 0
                for (let i = 0; i < this.cart.length;i++)
                {
                    if(this.cart[i] === id){
                        count++;
                    }
                }
                return count;
      },
      productFinder(id){
        for (let i =0; i< this.products.length;i++)
               {
                if(this.products[i].id===id)
                    return this.products[i];
               }
      },
       submitForm(){
                alert("Order placed!!")
            }
    },
    computed: {
            /*returns length of cart*/ 
            cartLength: function() {
                return this.cart.length || '';
            },
            canForm(){
                var letters = /^[A-Za-z]+$/;
                if (this.order.firstName.match(letters) )
                    if( this.order.lastName.match(letters)) 
                        if( this.order.number.length ===10)
                             return this.order.show=true;
                else
                        return this.order.show=false;
            },
        }
};
</script>