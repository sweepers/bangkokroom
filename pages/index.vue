<template>
  <div>
     <!--  http://128.199.95.64:81/assets/images/property/picture/RpAz6nVmsM_file_20190905164752.jpg
      http://128.199.95.64:81/assets/images/property/picture/nwkbVWCAqN_file_20190905131213.jpg"-->
  <b-container  fluid  >
  <hooper v-if="property_hl.length > 0">
    <slide v-for="pro in property_hl">
      <img  v-lazy="'http://128.199.95.64:81/assets/images/highlight-property/picture/'+pro.highlight_image" data-loading="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/0.16.1/images/loader-large.gif" style="width:100%; position: absolute; " />
     
      <b-container class="rel-pro" >
        <div  class="property_highlight">
          <h2>{{ pro.property_code }} - {{ pro.property_pin_name }} </h2>
          <div class="highlight-detail">
            <star-rating :rating="pro.property_rating" v-bind:star-size="20" read-only	></star-rating>
            <div class="cardFeature">
              <font-awesome-icon icon="map-marker-alt" /> {{ pro.zone.zone_name }} 
              <font-awesome-icon icon="train" /> {{ pro.bts.bts_name }} {{ pro.property_pin_to_bts }} M.<br />
              <font-awesome-icon icon="bed" />  {{ pro.property_bedroom }} <font-awesome-icon icon="cube" />   {{ pro.property_area_info }} m<sup>2</sup>
            
            </div>
            <div class="cardPrice">
              ฿{{ pro.property_sell_price | numFormat }} 
            </div>
          </div>
          
        </div>
      </b-container>
      
    
    </slide>
    
    <hooper-navigation slot="hooper-addons"></hooper-navigation>
  </hooper>
  </b-container>
  <!--<div class="after_banner">
    <div class="h-title osLight"></div>
  </div>-->
  <Search />
    <b-container>
      <b-row>
        <b-col cols="12" class="padding-30 text-center">
            <h3>Featured Rent</h3>
        </b-col>
      </b-row>
      <b-row v-if="pf_rents.length > 0" >
        <b-col v-for="pro in pf_rents" sm="12"  lg="4" >
          <nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name.replace(' ','_')" >
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
              <div class="price">
                {{ pro.property_rent_price | numFormat }} ฿ / Mo
              </div>
               <div class="property_code_list">{{ pro.property_code }}</div>  
              <div class="property_detail">   <star-rating :rating="pro.property_rating" v-bind:star-size="12" read-only class="rating_list" 	></star-rating> </div>
              <div style="clear:both;"></div>
               <nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name.replace(' ','_')" ><div class="p-name">{{ pro.property_pin_name }}</div></nuxt-link>
             
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
  
    </b-container>

    <b-container>
      <b-row>
        <b-col cols="12" class="padding-30 text-center">
            <h3>Featured Sale</h3>
        </b-col>
      </b-row>
      <b-row v-if="pf_sales.length > 0" >
        <b-col v-for="pro in pf_sales" sm="12"  lg="4" >
           <nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name.replace(' ','_')" >
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
               <div class="propWidget-PropertyAvatar" >
                <div class="propWidget-avatar" v-if="pro.gallery_pin.length > 0"  :style="'background-image: url(http://128.199.95.64:81/assets/images/property-pin/picture/'+pro.gallery_pin[0].gallery_image"></div>
              </div>
              <div class="property_code_list">{{ pro.property_code }}</div>  
                <div class="price">
                {{ pro.property_sell_price | numFormat }} ฿
                </div>
              <div class="property_detail">   <star-rating :rating="pro.property_rating" v-bind:star-size="12" read-only class="rating_list" 	></star-rating> </div>
              <div style="clear:both;"></div>
              <div class="p-name"> <nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name.replace(' ','_')" >{{ pro.property_pin_name }} </nuxt-link></div> 
             
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
  
    </b-container>



    <b-container>
      <b-row>
        <b-col cols="12" class="padding-30 text-center">
            <h3>Blog</h3>
        </b-col>
      </b-row>
      <b-row v-if="blogs.length > 0" >
        <b-col v-for="blog in blogs" sm="12"  lg="4" >
          
          <hooper class="photo" style="height:210px !important;" >
            <slide v-if="blog.blog_image" >
                <img  :src="'http://128.199.95.64:81/assets/images/blog/picture/'+blog.blog_image" class="img_footer" />
            </slide>
            <slide v-else>
              <img src="http://128.199.95.64:81/assets/images/default/property/picture.png" class="img_footer" /> 
            </slide>
          </hooper>
          
          
          <div class="property_l">
            <div class="inner">
              
              <div class="p-name">{{ blog.blog_tittle }}</div> 
              <div style="clear:both"></div>
              <div class="property_code_list">{{ blog.category_name }}</div> 
              <div style="clear:both"></div>
              <div class="cardAddress" > {{ blog.blog_sub_detail }}</div>
            </div>
              
              
              <button class="btn-enq"><font-awesome-icon icon="plus" /> Read More</button>
          </div>
            
          
        </b-col>
        
      </b-row>
  
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
        property_hl:[],
        pf_sales:[],
        pf_rents:[],
        blogs:[]
      }
     
   },
  components: {
    Logo,
    Header,
    Hooper,
    Slide,
    HooperNavigation,
    StarRating,
    Search
  },
  created(){
    this.gethighligh()
    this.getpropSale()
    this.getpropRent()
    this.getblog()
  },
  methods:{
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
    async getpropSale(){
      let prop =   this.$axios.get('/api/property?limit=6&featured=1&action=Sale').then((response) =>{
         this.pf_sales = response.data
         console.log('response',response);
        
        //alert(response)
      }).catch(function(error){
        //console.log('erro',error);
        //alert(error)
      })
      //console.log('index',prop);
    },
    async getblog(){
      //this.$axios.setHeader('crossDomain', true)
       //this.$axios.setToken('XCTCfz63MMKiac7uuWdRxcD2JhU+BGx77ta4tij5D55dMh7NqYTzbMLL+zU+OuK4785btUlYzOQhKCA4VxsVAc8vLSgl/f6YJVH8Bmx6ZVfoGU5lYAsbqlRdT79z0gN1m22+FHdxS4n1L4dnBTs9fVHYPWUNro0zwiaMjG33c/E=', 'auth')
       let prop =   this.$axios.get('/api/blog?limit=6').then((response) =>{
         console.log('highlight',response);
          this.blogs = response.data
        //alert(response)
      }).catch(function(error){
        //console.log('erro',error);
        //alert(error)
      })
      //console.log('index',prop);
    },
    async getpropRent(){
      let prop =   this.$axios.get('/api/property?limit=6&featured=1&action=Rent').then((response) =>{
         this.pf_rents = response.data
         console.log('response',response);
        
        //alert(response)
      }).catch(function(error){
        //console.log('erro',error);
        //alert(error)
      })
      //console.log('index',prop);
    }
  }
  
}
</script>


