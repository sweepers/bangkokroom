<template>
  <div>
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
     <b-container>
       <b-row>
          <b-col sm="12" lg="9">
            <ol class="breadcrumb">
              <li>
                <nuxt-link to="/" >Home</nuxt-link>
              </li>
              <li class="active"> 
                Contact us
              </li>
            </ol>
            <div>
              <h2>Findbangkokroom</h2>
              <b-row>
                <b-col sm="12" lg="5">
                  <h4>Contact Details</h4>
                  <div class="contact-details"><font-awesome-icon icon="envelope" /> mail@findbangkokroom.com</div>
                  <div class="contact-details"><font-awesome-icon icon="building" /> + 66 (0) 990 955 535</div>
                  <div class="contact-details"> <font-awesome-icon icon="phone-alt" />  66 (0) 816 157 487, +66 (0) 885 852 878</div>
                  <div class="contact-details"><font-awesome-icon icon="fax" /> +66 (0) 266 360 40</div>
                  <div class="contact-details"><font-awesome-icon icon="map-marker-alt" /> 888 Polaris tower Sukhumvit soi 20 , Klongtoey Bangkok 10110</div>
                  
                  
                </b-col>
                <b-col sm="12" lg="3">
                  <h4>Follow Us</h4>
                  <div class="contact-details"><a href="https://www.facebook.com/Findbkkroom" target="_blank"><font-awesome-icon :icon="['fab','facebook']"  /> Facebook</a></div>
                  <div class="contact-details"><a href="https://plus.google.com/+Findbangkokroom" target="_blank"  ><font-awesome-icon :icon="['fab','google-plus']" /> Google +</a></div>
                </b-col>
                <b-col sm="12" lg="4">
                  <h4>LINE QR Code</h4>
                   <img src="~/assets/images/qr-code.jpg" height="120px"  />
                </b-col>
              </b-row>
            </div>
              <hr />
        <h4>Send Us a Message</h4>
        <form class="contactPageForm">
          <b-row>
            <b-col cols="12">
              <div class="form-group">
                <label>Name <span>*</span></label>
                <input type="text" name="contact_name" class="form-control" placeholder="Enter your name" value="" />
              </div>
            </b-col>
             <b-col cols="6">
              <div class="form-group">
                <label>Email</label>
                <input type="text" name="contact_email" class="form-control" placeholder="Enter your email" value="" />
              </div>
            </b-col>
             <b-col cols="6">
              <div class="form-group">
                <label>Phone</label>
                <input type="text" name="contact_phone" class="form-control" placeholder="Enter your phone number" value="" />
              </div>
              
            </b-col>
             <b-col cols="12">
              <div class="form-group">
                <label>Subject <span>*</span></label>
                <input type="text" name="contact_subject" class="form-control" placeholder="Enter the subject" value="" />
              </div>
            </b-col>
             <b-col cols="12">
              <div class="form-group">
                <label>Message <span>*</span></label>
                <textarea class="form-control" placeholder="Type your message" rows="3" ></textarea>
              </div>
            </b-col>
            <b-col cols="12">
              <div class="form-group">
                <button class="btn btn-green">Send Message</button>
              </div>
            </b-col>
          </b-row>

        </form> 
          <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3875.7916698193267!2d100.5617013152786!3d13.731059201472132!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x30e29f02d1d35e49%3A0x1d2e6391e6f3f0f!2swww.findbangkokroom.com%20condo%20for%20rent%20condo%20for%20sale%20apartment%20sukhumvit%20Bangkok%20Real%20estate%20agency!5e0!3m2!1sth!2sth!4v1573051032871!5m2!1sth!2sth" width="100%" height="450" frameborder="0" style="border:0;" allowfullscreen=""></iframe>
          </b-col>
           <b-col sm="12" lg="3">
             <h4>Feature Properties</h4>
             <b-row v-if="pf_feature.length > 0" v-for="pro in pf_feature">
                <b-col  cols="3">
                    <nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name" >
                <img v-if="pro.gallery.length > 0" :src="'http://128.199.95.64:81/assets/images/property/picture/'+pro.gallery[0].gallery_image" class="img_footer" />
                <img v-else src="http://128.199.95.64:81/assets/images/default/property/picture.png" class="img_footer" />
                    </nuxt-link>
                </b-col>
                <b-col  cols="9" >
                    <div class="info">
                        <div class="name"><nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name" >{{ pro.property_pin_name }}</nuxt-link></div> 
                        <div class="property_code">{{ pro.property_code }}</div>   
                        <div class="address" v-if="pro.zone_id>0">{{ pro.zone.zone_name }}</div>
                        <div class="address" v-if="pro.bts_id >0">{{ pro.bts.bts_name }} {{ pro.property_pin_to_bts }} M.</div>
                        <div class="price">
                        {{ pro.property_sell_price | numFormat }} ฿
                        </div>
                    </div>
                    
                
                </b-col>
            </b-row>
            <h4>Lasted Properties</h4>
             <b-row v-if="lasted_prop.length > 0" v-for="pro in lasted_prop">
                <b-col  cols="3">
                    <nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name" >
                <img v-if="pro.gallery.length > 0" :src="'http://128.199.95.64:81/assets/images/property/picture/'+pro.gallery[0].gallery_image" class="img_footer" />
                <img v-else src="http://128.199.95.64:81/assets/images/default/property/picture.png" class="img_footer" />
                    </nuxt-link>
                </b-col>
                <b-col  cols="9" >
                    <div class="info">
                        <div class="name"><nuxt-link :to="'/properties/'+pro.property_code+'-'+pro.property_pin_name" >{{ pro.property_pin_name }}</nuxt-link></div> 
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
       
    </b-container>
  </div>
 
     
     
</b-container>
  
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
        pf_feature:[],
        lasted_prop:[],
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
    this.getFeatures()
    this.getprop()
   
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
    getprop(){
            //var parent = this;
             this.$axios.get('/api/property?limit=5&offset=0&order_by=property_id,DESC&status=1&action=Sale').then((response) =>{
               
                this.lasted_prop =   response.data
                 //console.log('response_2', this.lasted_prop );
                //alert(response)
            }).catch((error) =>{
                //console.log('erro',error);
                //alert(error)
            })
           // console.log('test',prop.vl);
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
    
    
  }
}
</script>


