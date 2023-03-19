<template>
  <div class="q-pa-md">
    <q-markup-table>
      <thead>
        <tr>
          <th class="text-left">account_id</th>
          <th class="text-right">name</th>
          <th class="text-right">email</th>
          <th class="text-right">phone</th>
          <th class="text-right">password</th>
          <th class="text-right">delete</th>

        </tr>
      </thead>
      <tbody>
        <tr v-for="user in userdetail" :key="user.account_id">
          <td class="text-left">{{ user.account_id }}</td>
          <td class="text-right">{{ user.name  }}</td>
          <td class="text-right">{{ user.email  }}</td>
          <td class="text-right">{{ user.phone  }}</td>
          <td class="text-right">{{ user.password }}</td>
          <td class="text-right"><button @click="deleteData(user.account_id)">delete</button></td>

        </tr>

      </tbody>
    </q-markup-table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      api:'http://localhost/myaccount2/api-account2.php',
      userdetail:''
    }
  },

  methods:{
    getdata(){
      var t = this;
      axios.post(this.api,{
        action:"getall"
      }).then(res=>{
        console.log(res.data)
        t.userdetail=res.data
      })
    },
    deleteData(id){
      console.log("deleting");
      axios.post(this.api,{
        action:"delete",
        id1:id
      }).then(res=>{
        console.log(res.data);

      })

    }
  },
  created(){
    this.getdata()
  }

}
</script>

<style>

</style>
