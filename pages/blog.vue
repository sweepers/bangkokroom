<template>

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
  
</template>

<script>
import Logo from '~/components/Logo.vue'
import Header from '~/components/Header.vue'
export default {
  components: {
    Logo,
    Header
  },
   data(){
      return {
        
        blogs:[]
      }
     
   },
   created(){

    this.getblog()
  },
  methods:{
   
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
    }
    
  }
}
</script>


