<template>
    <main>
        <div class="search">
            <input id="searchS" placeholder="search..." type="text" v-model="search" @keyup="searcher" >
            <br>
            <i class="fa-solid fa-hat-wizard"></i>
            <input type="radio" id="Assend" name="order" value="Assending" @click=" sorter">Ascending
            <input type="radio" id="Dessend" name="order" value="Dessending" @click=" sorter">Descending:
            <input type="radio"  id="Price" name="oType" value="Price" @click=" sorter">Price
            <input type="radio" id="location" name="oType" value="location" @click=" sorter">location
            <input type="radio" id="Subject" name="oType" value="Subject" @click=" sorter">Subject
            <input type="radio" id="Space" name="oType" value="Space" @click=" sorter">Space
        </div>
        <!-- Div container for displaying products/lessons -->
        <div class="productss" >
                <div class="product" v-for="product in products" :key="product.id" v-if="product.show===true">
                    <figure>
                    <img height="200px" width="180px" v-bind:src="product.image">
                    </figure>
                    <!-- content of each product -->
                    <div id="content"> 
                        <p >Subject: <b>{{product.title}}</b></p>
                        <p> City: <b>{{product.location}}</b></p>
                        <p>Price: <b>{{product.price}}</b></p>
                        <p>Space: <b>{{product.quantity}}</b></p>
                        <!-- rating made using v-for -->
                        <div>
                            <br>
                            <!-- <span v-for="n in product.rating"><i class="fa-solid fa-star"></i></span>
                            <span v-for="n in 5-product.rating"><i class="fa-regular fa-star"></i></span> -->
                        </div>
                       
                        <button id="Mbutton" @click='addProduct(product)' v-bind:disabled="!canAdd(product)">Add</button>
                        <span v-if="product.quantity === 0">
                             All out!!
                        </span>
                        <span v-else-if="product.quantity  < 5">
                             only {{product.quantity }} left!
                        </span>
                        <span v-else>  Buy now!!</span>
                    </div>
                </div>
        </div>
    </main>
</template>
<script>
export default{
    name:"ProductList",
    props:{ products:{type: Array, required: true}, cart:{type: Array, required: true}},
    data(){
        return{
            search:""
        }
    },
    methods: {
      addProduct(product){
        this.$emit('addProduct',product);
      },
      canAdd(product){
        return product.
                quantity!=0 
        // this.$emit('canAdd',product);
      },
      searcher(){
                
                this.products.forEach((element) => {
                    
                    let tText=element.title.toLowerCase();
                    let lText=element.location.toLowerCase();
                    if(!this.search && this.search ==="")
                        element.show= true;
                    let i=0;
                    while(this.search && i < this.search.length )
                    {
                        let sText =this.search.toLowerCase();
                        if (sText[i]===tText[i]|| sText[i]===lText[i])
                            element.show= true;
                        else{
                            element.show = false;
                            break;
                        }
                        i++
                    }
                });
            },
            /*sorting function*/ 
            sorter()
            {
                if(document.getElementById('Price').checked===true)
                {
                    function compare(a,b){
                        if (a.price > b.price)
                            return 1;
                        if (a.price < b.price)
                            return -1
                        return 0;
                    }
                     this.products.sort(compare);
                }
                else if(document.getElementById('location').checked===true)
                {
                    function compare(a,b){
                        if (a.location > b.location)
                            return 1;
                        if (a.location < b.location)
                            return -1
                        return 0;
                    }
                     this.products.sort(compare);
                }
                else if(document.getElementById('Subject').checked===true)
                {
                    function compare(a,b){
                        if (a.title > b.title)
                            return 1;
                        if (a.title < b.title)
                            return -1
                        return 0;
                    }
                     this.products.sort(compare);
                }
                else if(document.getElementById('Space').checked===true)
                {
                    function compare(a,b){
                        if (a.quantity > b.quantity)
                            return 1;
                        if (a.quantity < b.quantity)
                            return -1
                        return 0;
                    }
                     this.products.sort(compare);
                }

                if(document.getElementById('Assend').checked===true)
                ;
                else if(document.getElementById('Dessend').checked===true)
                {
                    console.log(document.getElementById('Dessend').value)
                    this.products.reverse();
                }

            }  
    },
};
</script>