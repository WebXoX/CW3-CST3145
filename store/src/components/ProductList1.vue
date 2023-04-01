<!-- <template>
    <main>
        <div class="search">
            <input id="searchS" type="text" v-model="search" @keyup="searcher(products)" >
            <br>
           
            <input type="radio" id="Assend" name="order" value="Assending" checked="checked" @click=" sorter(products)">Assending
                <input type="radio" id="Dessend" name="order" value="Dessending" @click=" sorter(products)">Dessending:
                <input type="radio"  id="Price" name="oType" value="Price" checked="checked" @click=" sorter(products)">Price
                <input type="radio" id="location" name="oType" value="location" @click=" sorter(products)">location
                <input type="radio" id="Subject" name="oType" value="Subject" @click=" sorter(products)">Subject
                <input type="radio" id="Space" name="oType" value="Space" @click=" sorter(products)">Space

        </div>
        <div class="productss">
                <div class="product" v-for="product in products"  style="border: solid black 2px; border-radius: 40px; height: 200px; width: 300px;" :key="product.id"> 
                    <figure>
                    <img height="100px" v-bind:src="product.image">
                    </figure>
                    <div id="content">
                        <p >Subject: <b>{{product.title}}</b></p>
                        <p> City: {{product.location}}</p>
                        <p>Price: {{product.price}}</p>
                        <p>space: {{product.quantity}}</p>
                        <div>
                            <span v-for="n in product.rating" :key="n"><i class="fa-regular fa-star"></i></span>
                        <span v-for="n in 5-product.rating" :key="n"><i class="fa-solid fa-star"></i></span>
     
                        </div>
                       
                        <button id="Mbutton" @click='addItem(product)' v-bind:disabled="!canAdd(product)">Add</button>
                        <span v-if="product.quantity === cartCount(product.id)">
                            All out!!
                        </span>
                        <span v-else-if="product.quantity  < 5">
                            only {{product.quantity }} left!
                        </span>
                        <span v-else>Buy now!!</span>
                    </div>
                </div>
        </div>
    </main>
</template>
<script>
import { boolean } from 'webidl-conversions';

export default{
    name:"ProductList",
    props:{ showProduct:{type: boolean, required: true}, products:{type: Array, required: true}},
    data(){
        return{
            search:''
        }
    },
    methods: {
        addItem(product){
        this.$emit('addItem',product);
      },
      canAdd(product){
        this.$emit('canAdd',product);
      },
      cartCount(id){
        this.$emit('canAdd',id);
      },
      sorter(){
        this.$emit("sorter",products)
      },
      searcher(){
        this.$emit("searcher",products)
      }
    }
};
</script> -->