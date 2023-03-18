<script >
import { parse, format } from 'date-fns';
import { formatDistanceToNow } from 'date-fns';

  export default{
    name:'Posts',
    data(){
      return{
        posts:[],
      };
    },
    mounted(){
      this.load();
    },
    methods:{
      load(){
        //fetch the posts 
        const url = 'https://www.reddit.com/r/rarepuppers/.json'
        fetch(url)
          .then(response => response.json())
          .then(result => {
            result.data.children.forEach(child =>{
              child.showImage = false ;
            });
            this.posts = result.data.children;
          });
      },
      formatDate(date) {
        const parsedDate = new Date(date * 1000);
        return format(parsedDate, 'MMMM d, yyyy');
      },
      formatDateToNow(date){
        const dateToNow = new Date(date*1000);
        return formatDistanceToNow(dateToNow);
      },
      createLink(path){
        return `https://www.reddit.com/${path}`
      },
      showImg(post){
        post.data.showImage =!post.data.showImage
      },
      isImg(post){
        return post.data.url.match(/\.(jpg|png|jpeg|bpm)$/);
      }

    },
  };
</script>

<template>
  <div class="hello mt-3">
    <ul class="list-unstyled">
      <li v-for="post in posts" class="media m-3">
        <img class="mr-3" :src="post.data.thumbnail" alt="Generic placeholder image">
        <div class="media-body">
            <h5 class="mt-0 mb-1"><a :href="createLink(post.data.permalink)" target="_blank">{{post.data.title}}</a></h5>
            <p>
              <h3 class="text-danger">
                <svg xmlns="http://www.w3.org/2000/svg" height="32px" viewBox="0 0 24 24" width="24px" fill="#ffffff"><path d="M0 0h24v24H0V0z" fill="none"/><path d="M4 12l1.41 1.41L11 7.83V20h2V7.83l5.58 5.59L20 12l-8-8-8 8z"/></svg>
                {{ post.data.ups }}
              </h3>
            <p>created {{formatDateToNow(post.data.created)  }} ago by {{ post.data.author }}</p>
              <span class="badge badge-pill badge-primary">{{post.data.num_comments}} comments</span>
              <button
              v-if="isImg(post)" 
              @click="post.showImage = !post.showImage" type="button" class="btn btn-primary">
              {{ post.showImage ? 'Hide' : 'Show' }} Image
              </button>
              <div v-if="post.showImage">
                <img :src="post.data.url" alt="">
              </div>
            </p>
          </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>

.media {
  display: flex;
  align-items: center;
}
.media-body{
  margin-left: 10px;
}


</style>