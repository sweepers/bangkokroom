<template>
  <div>
    
  
  <Search />
    <b-container class="prop-list">
      
      <b-row v-if="lists.length > 0" >
        <b-col v-for="pro in lists" sm="12"  lg="4" >
           <nuxt-link :to="'/properties/'+pro.property_code+'-'" >
          <hooper class="photo" style="height:210px !important;" >
            <slide v-if="pro.gallery.length > 0"  v-for="gal in pro.gallery">
                <img v-if="pro.gallery.length > 0" :src="'http://128.199.95.64:81/assets/images/property/picture/'+gal.gallery_image" class="img_footer" />
            </slide>
            <slide v-else>
              <img src="http://128.199.95.64:81/assets/images/default/property/picture.png" class="img_footer" /> 
            </slide>
          </hooper>
           </nuxt-link>
          
          <div class="property_l">
            <div class="inner">
              <div class="propWidget-PropertyAvatar"  >
                <div class="propWidget-avatar"  v-if="pro.gallery_pin.length > 0" :style="'background-image: url(http://128.199.95.64:81/assets/images/property-pin/picture/'+pro.gallery_pin[0].gallery_image"></div>
              </div>
              <div class="price" v-if="pro.property_rent_price > 0">
                {{ pro.property_rent_price | numFormat }} ฿ / Mo
              </div>
              <div class="price" v-if="pro.property_sell_price > 0">
                {{ pro.property_sell_price | numFormat }} ฿
              </div>
               <div class="name" v-if="pro.property_pin_name"><nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name.replace(' ','_')" >{{ pro.property_pin_name }}</nuxt-link></div> 
               <div class="property_code_list">{{ pro.property_code }}</div>  
              <div class="property_detail">   <star-rating :rating="pro.property_rating" v-bind:star-size="12" read-only class="rating_list" 	></star-rating> </div>
              <div style="clear:both;"></div>
             
              <div style="clear:both"></div>
              <div class="cardAddress" v-if="pro.bts_id >0"><font-awesome-icon icon="train" /> {{ pro.bts.bts_name }} {{ pro.property_pin_to_bts }} M.</div>
            </div>
            <b-row class="list_bottom">
              <b-col cols="4"><font-awesome-icon icon="bed" />  {{ pro.property_bedroom }}</b-col>
              <b-col cols="4"> {{ pro.property_area_info }}m<sup>2</sup></b-col>
              <b-col cols="4"><button class="btn-enq"><font-awesome-icon icon="heart" /></button></b-col>
            </b-row>
              
              
          </div>
            
          
        </b-col>
        
      </b-row>
       <b-pagination v-model="currentPage" :total-rows="rows" :limit="limit"  @change="change_page"></b-pagination>
    </b-container>

    

  </div>
  
  
</template>

<script>
import Logo from '~/components/Logo.vue'
import Header from '~/components/Header.vue'
import StarRating from 'vue-star-rating'
import Search from '~/components/Search.vue'
import {
  Hooper,
  Slide,
  Progress as HooperProgress,
  Pagination as HooperPagination,
  Navigation as HooperNavigation
} from 'hooper';
export default {
   data(){
      return {
        keywords:'',
        lists:[],
        limit:12,
        offset:0,
        page:1,
        currentPage:1,
        rows: 100,
       
      }
     
   },
  components: {
    Logo,
    Header,
    Hooper,
    Slide,
    HooperNavigation,
    Search,
    StarRating
  },
  created(){
    //console.log('url',this.$nuxt.$route.query.test);
    this.getlists()
  },
  methods:{
    change_page(page){
      let offset = this.limit*(page-1)
      this.offset = offset;
      console.log('page',page);
      this.getlists();
    },
    async gethighligh(){
      //this.$axios.setHeader('crossDomain', true)
       //this.$axios.setToken('XCTCfz63MMKiac7uuWdRxcD2JhU+BGx77ta4tij5D55dMh7NqYTzbMLL+zU+OuK4785btUlYzOQhKCA4VxsVAc8vLSgl/f6YJVH8Bmx6ZVfoGU5lYAsbqlRdT79z0gN1m22+FHdxS4n1L4dnBTs9fVHYPWUNro0zwiaMjG33c/E=', 'auth')
       let prop =   this.$axios.get('/api/property?highlight=1').then((response) =>{
         console.log('highlight',response);
          this.property_hl = response.data
        //alert(response)
      }).catch(function(error){
        //console.log('erro',error);
        //alert(error)
      })
      //console.log('index',prop);
    },
    async getlists(){
      let prop =   this.$axios.get('/api/property?limit='+this.limit+'&offset='+this.offset+'&action=Sale,Rent&keywords='+this.keywords).then((response) =>{
         this.lists = response.data
         this.rows =  response.headers['x-total-count']
         console.log('response',response);
        
        //alert(response)
      }).catch(function(error){
        //console.log('erro',error);
        //alert(error)
      })
      //console.log('index',prop);
    },
  
  }
  
}
</script>


