<template>
  <div v-for="post in postData" :key="post.id">
      <h4>{{post.title}}</h4>
    <article>
        {{post.body}}
    </article>
    <hr>
  </div>
</template>

<script>
export default {
name:"Posts",
data(){
    return{
        postData:undefined
    }
},
mounted(){
    const url="https://jsonplaceholder.typicode.com/posts";
    fetch(url)
    .then(res=>res.json())
    .then(data=>{
        this.postData=data
        console.log(data)
    })
}
}
</script>

<style>

</style>