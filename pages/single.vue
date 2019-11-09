<template>
<div>
<b-container  fluid  >
  <hooper v-if="item.gallery" :settings="cardsHooper">
    <slide v-for="gal in item.gallery">
      <img  v-lazy="'http://128.199.95.64:81/assets/images/property/picture/'+gal.gallery_image" data-loading="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/0.16.1/images/loader-large.gif" style="height:480px;" />
     
    
    </slide>
    
    <hooper-navigation slot="hooper-addons"></hooper-navigation>
  </hooper>
  </b-container>
    <div class=" property-highlight">
        <b-container >
            <b-row>
                <b-col  sm="6" lg="2" class="PropertyPinAvatarContainer">
                    <div class="PropertyPinAvatar">
                        <a><div class="property-pin-avatar"  v-if="item.gallery_pin" :style="'background-image: url(http://128.199.95.64:81/assets/images/property-pin/picture/'+item.gallery_pin[0].gallery_image"></div></a>
                    </div>
                </b-col>
                <b-col sm="6" lg="5">
                    <p v-if="item.type">{{ item.type.type_name }}</p>
                    <h3>{{ item.property_pin_name }}</h3>
                    <span v-if="item.bts"><font-awesome-icon icon="train" /> {{ item.bts.bts_name }}</span>
                    <span >{{ item.property_pin_to_bts }} meters</span>
                     <span v-if="item.zone"><font-awesome-icon icon="map-marker-alt" /> {{ item.zone.zone_name }}</span>
                </b-col>
                 <b-col sm="6" lg="5">
                     <h1 ><template v-if="item.property_rent_price > 0">฿ {{ item.property_rent_price | numFormat }} / Mo</template> <template v-if="item.property_sell_price > 0">฿ {{ item.property_sell_price | numFormat }}</template></h1>
                    
                     <h3>
                     <span><font-awesome-icon icon="bed" />  {{ item.property_bedroom }}</span>
                      <span><font-awesome-icon icon="bath" />  {{ item.property_bahtroom }}</span>
                      <span><font-awesome-icon icon="cube" />  {{ item.property_area_info }} m<sup>2</sup></span>
                      </h3>
                 </b-col>
            </b-row>
        </b-container>
    </div>
    <b-container>
        <b-row>
            <b-col sm="12" lg="8">
                
                <div class="property-menu-bar">
                    <b-button-group  class="btn-group-justified">
                        <b-button  v-scroll-to="'#Feature'" class="btn-group">Feature</b-button>
                        <b-button  v-scroll-to="'#Gallery'" class="btn-group">Full Gallery</b-button>
                        <b-button v-scroll-to="'#map'" class="btn-group">Area Map</b-button>
                    </b-button-group>
                </div>
                <div id="Feature" class="property-header" v-if="item">
                    <h2 v-if="item.f_rooms ">Room Featured</h2>
                    <b-row v-if="item.f_rooms">
                        <b-col v-for="feature in item.f_rooms" sm="6" lg="4">
                            {{ feature.facility_name }}
                        </b-col>
                    </b-row>
                     <h2 v-if="item.p_features" style="padding-top:20px;">Property Featured</h2>
                    <b-row v-if="item.p_features">
                        <b-col v-for="feature in item.p_features" sm="6" lg="4">
                            {{ feature.facility_name }}
                        </b-col>
                    </b-row>
                </div>
                <div id="Gallery" v-if="item.gallery">
                    <h2>Full Gallery</h2>
                  
                    <LightGallery
                        :images="images"
                        :index="index"
                        :disable-scroll="true"
                        @close="index = null"
                    />
                    <b-row>
                        <b-col cols="4"  v-for="(thumb, thumbIndex) in item.gallery" :key="thumbIndex"
        @click="index = thumbIndex">
                             <img :src="'http://128.199.95.64:81/assets/images/property/picture/'+thumb.gallery_image" class="thumb">
                        </b-col>
                    </b-row>
   
                
                  
                </div>
                <div id="map">
                    <h2>Area Map</h2>
                    <iframe :src="'https://maps.google.com/maps?q='+item.property_pin_lattitude+','+item.property_pin_longitude+'&hl=en&z=14&amp;output=embed'" width="100%" height="450" frameborder="0" style="border:0;" allowfullscreen=""></iframe>
                  

                  
                </div>
                <h2 class="property-header">Similar Area</h2>
                 <b-row v-if="p_areas.length > 0" >
                    <b-col v-for="pro in p_areas" sm="12"  lg="6" >
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
            </b-col>
            <b-col sm="12" lg="4">
                <b-row>
                    <b-col cols="6">
                        <p>ID: {{ item.property_code }}</p>
                        <star-rating :rating="item.property_rating" v-bind:star-size="12" read-only class="rating_list" 	></star-rating>   <font-awesome-icon icon="eye" /> {{ item.total_view }}
                    </b-col>
                    <b-col cols="6">
                        <button class="btn-enquiry"><font-awesome-icon icon="heart" /></button>
                    </b-col>
                </b-row>
                <b-row>
                    <b-col cols="12">
                        <form class="enquiry-form row">
                            <b-col cols="12">
                                <label class="pull-right">Contact Our Agent</label>
                            </b-col>
                            <b-col cols="12">
                                <div class="form-group text-center">
                                    <img src="http://128.199.95.64:81/assets/images/default/user/avatar.png" class="agentAvatar ng-scope" />
                                </div>
                                
                            </b-col>
                            <b-col cols="12">
                                <div class="form-group">
                                    <label>Name <span class="text-red">*</span></label>
                                    <input type="text" name="contact_name" placeholder="Enter Your Name" class="form-control" value="" />
                                </div>
                            </b-col>
                            <b-col sm="12" lg="6">
                                <div class="form-group">
                                    <label>Email</label>
                                    <input type="text" name="contact_email" placeholder="Enter Your Email" class="form-control" value="" />
                                </div>
                            </b-col>
                            <b-col sm="12" lg="6">
                                <div class="form-group">
                                    <label>Phone</label>
                                    <input type="text" name="contact_phone" placeholder="Enter Your Phone" class="form-control" value="" />
                                </div>
                            </b-col>
                             <b-col cols="12">
                                <div class="form-group">
                                    <label>Subject <span class="text-red">*</span></label>
                                    <input type="text" name="contact_subject"  class="form-control" :value="'Interested in The Empire Place #'+item.property_code" />
                                </div>
                            </b-col>
                            <b-col cols="12">
                                <div class="form-group">
                                    <label>Message <span class="text-red">*</span></label>
                                   
                                    <textarea class="form-control" rows="3" v-if="item.property_pin_name">I am Interested The Empire Place #{{ item.property_code }} http://www.findbangkokroom.com/properties/{{ item.property_code }}-{{ item.property_pin_name.replace(' ','_') }} {{ item.property_bedroom }} bedroom Rent ฿ {{ item.property_rent_price | numFormat }}  Sale ฿ {{ item.property_sell_price | numFormat }} please let me know when is possilbe to visit</textarea>
                                   
                                    
                                </div>
                            </b-col>
                            <b-col cols="12">
                                <div class="form-group">
                                    <button class="btn btn-green">Send Message</button>
                                </div>
                            </b-col>
                        </form>
                    </b-col>
                    <b-col cols="12">
                       <h2 class="property-header">Feature Properties</h2>
                       <b-row v-if="pf_feature.length > 0" v-for="pro in pf_feature">
                            <b-col  cols="3">
                                <nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name.replace(' ','_')" >
                            <img v-if="pro.gallery.length > 0" :src="'http://128.199.95.64:81/assets/images/property/picture/'+pro.gallery[0].gallery_image" class="img_footer" />
                            <img v-else src="http://128.199.95.64:81/assets/images/default/property/picture.png" class="img_footer" />
                                </nuxt-link>
                            </b-col>
                            <b-col  cols="9" >
                                <div class="info">
                                    <div class="name"><nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name.replace(' ','_')" >{{ pro.property_pin_name }}</nuxt-link></div> 
                                    <div class="property_code">{{ pro.property_code }}</div>   
                                    <div class="address" v-if="pro.zone_id>0">{{ pro.zone.zone_name }}</div>
                                    <div class="address" v-if="pro.bts_id >0">{{ pro.bts.bts_name }} {{ pro.property_pin_to_bts }} M.</div>
                                    <div class="price">
                                    {{ pro.property_sell_price | numFormat }} ฿
                                    </div>
                                </div>
                                
                            
                            </b-col>
                        </b-row>
                    </b-col>
                </b-row>
                
            </b-col>
           
        </b-row>
    </b-container>
</div>

</template>

<script>
import Logo from '~/components/Logo.vue'
import Header from '~/components/Header.vue'
import StarRating from 'vue-star-rating'

import {
  Hooper,
  Slide,
  Progress as HooperProgress,
  Pagination as HooperPagination,
  Navigation as HooperNavigation
} from 'hooper'
export default {
   data(){
      return {
        item:{},
        code:'',
        images: [],
        index: null,
        pf_feature:[],
        p_areas:[],
        cardsHooper: {
            itemsToSlide: 3,
            itemsToShow: 3.25,
            infiniteScroll: true
        }
       
      }
     
   },
  components: {
    Logo,
    Header,
    Hooper,
    Slide,
    HooperNavigation,
    
    StarRating
  },
  created(){
      //this.code = $this.$nuxt.$route.name
      //console.log('code',this.$route.params.slug );
      let slug = this.$route.params.slug.split('-');
      this.code = slug[0]
      //$nuxt.$route.path
    //console.log('url',this.code);
    this.getsingle()
    this.getFeatures()

  },
  methods:{

    async getsingle(){
      let prop =   this.$axios.get('/api/property/'+this.code).then((response) =>{
         this.item = response.data
         console.log('single',response);
        if(this.item.gallery){
           let galleries = []
           this.item.gallery.forEach(function(element) {
               let el = {}
                el.title = element.gallery_image
               el.url = 'http://128.199.95.64:81/assets/images/property/picture/'+element.gallery_image
               //console.log(element);
              //  console.log(element);
                galleries.push(el);
            });
             this.getParea(this.item.zone_id)
           // console.log('galleries', galleries);
            this.images = galleries;
            ///'http://128.199.95.64:81/assets/images/property/picture/'+thumb.gallery_image
        }
        //alert(response)
      }).catch(function(error){
        //console.log('erro',error);
        //alert(error)
      })
      //console.log('index',prop);
    },
    async getFeatures(){
      let prop =   this.$axios.get('/api/property?limit=5&featured=1&action=Sale,Rent').then((response) =>{
         this.pf_feature = response.data
         console.log('response',response);
        
        //alert(response)
      }).catch(function(error){
        //console.log('erro',error);
        //alert(error)
      })
      //console.log('index',prop);
    },
    async getParea(zone_id){
      let prop =   this.$axios.get('/api/property?limit=6&featured=1&action=Sale,Rent&zone_id='+zone_id).then((response) =>{
         this.p_areas = response.data
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
