<template>
  <div class="details container">
      <router-link to="/" class="btn btn-default">返回</router-link>
      <h1 class="page-herder">
          {{customer.name}}
        <span class="pull-right">
            <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">
                编辑
            </router-link>
            <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">
                删除
            </button>
        </span>
      </h1>
      <ul class="list-group">
          <li class="list-group-item"><span class="glyphicon glyphicon-earphone">{{customer.phone}}</span></li>
          <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customer.email}}</span></li>
      </ul>
      <ul class="list-group">
          <li class="list-group-item"><span class="glyphicon glyphicon-earphone">{{customer.education}}</span></li>
          <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customer.graduationschool}}</span></li>
          <li class="list-group-item"><span class="glyphicon glyphicon-earphone">{{customer.profession}}</span></li>
          <li class="list-group-item"><span class="glyphicon glyphicon-asterisk">{{customer.profile}}</span></li>
      </ul>
  </div>
</template>

<script>
export default {
  name: 'customerdetails',
  data () {
    return {
        customer:""
    }
  },
   methods: {
      fetchCustomers(id){
          this.$http.get("http://localhost:3000/users/"+id)
            .then((response)=>{
                console.log(response);
                // this.customer=response.body;
                this.customer=response.data;
            })
      },
      deleteCustomer(id){
        //   console.log(id);
        this.$http.delete("http://localhost:3000/users/"+id)
            .then((response)=>{
                this.$router.push({path:"/",query:{alert:"用户删除成功"}}) 
            })
      }
  },
  created(){
      this.fetchCustomers(this.$route.params.id);
  }
}
</script>

<style scoped>

</style>
 