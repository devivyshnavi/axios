<template>
  <div>
      <table class="table" border=1>
          <tr>
              <th>Sno</th>
              <th>Name</th>
              <th>Email</th>
              <th>Website</th>
              <th>Phone no</th>
            </tr>
            <tr v-for="(user,index) in userdata" .key="user.id">
                <td>{{index+1}}</td>
                <td>{{user.name}}</td>
                <td>{{user.email}}</td>
                <td>{{user.website}}</td>
                <td>{{user.phone}}</td>
                </tr>
      </table>
      </div>
</template>

<script>
import axios from 'axios';

export default {
name:"Users",
data(){
    return{
        userdata:undefined
    }
},
mounted(){
const url="https://jsonplaceholder.typicode.com/users";
axios.get(url)
.then(res=>{
    console.log(res.data)
    this.userdata=res.data
})
}
}
</script>

<style>

</style>