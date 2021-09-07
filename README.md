---
home: true
---
<template>
  <div class="__home_container">
    <el-row class="header">
      <div class="content">
         <div class="title">
            The Thinkium Developer Hub
         </div>
         <div class="desc">
            Welcome to the Thinkium developer hub. You'll find comprehensive guides and documentation to help you start working with Thinkium as quickly as possible, as well as support if you get stuck. Let's jump right in!
         </div>
         <div class="link-list">
           <!-- <img src="/images/TKM.png" alt="" class="link-img" > -->
           <a :href="item.link"  target="_blank" v-for="item in linkList"><img :src="$withBase(item.imgSrc)" alt="" class="link-img" ></a>
         </div>
      </div>
    </el-row>
    <el-row class="main content">
       <ul class="module-list" @click="toPath">
          <li class="module-item" v-for="item in moduleList" :data-path="item.path">
            <span>{{item.label}}</span>
          </li>
       </ul>
    </el-row>
  </div>
</template>

<script>
  export default {
   components: {

   },
   data () {
     return {
       linkList: [
         {link: 'https://www.thinkium.net', imgSrc: '/images/TKM.png'},
         {link: 'https://0.plus/Thinkiumofficial', imgSrc: '/images/Telgram.png'},
         {link: 'https://twitter.com/Thinkium_Chain', imgSrc: '/images/Twitter.png'},
         {link: 'https://thinkiumfoundation.medium.com/thinkium-blockchain-9e03c36fb7af', imgSrc: '/images/Medium.png'},
         {link: 'https://www.reddit.com/r/Thinkium/', imgSrc: '/images/Reddit.png'},
         {link: 'https://github.com/ThinkiumGroup', imgSrc: '/images/Github.png'},
       ],
       moduleList: [
         {label: 'Development', path: '/en/DApp Development/RPC/Introduction'},
       ]
     }
   },
   methods: {
     toPath(e){
       let {path} = e.target.dataset;
       this.$router.push(path)
     }
   },
   mounted(){
     console.log('---this.$page.frontmatter', this.$page.frontmatter);
     
   }
 }
</script>

<style scoped lang="scss">

</style>



