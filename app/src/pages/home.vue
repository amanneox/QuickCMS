<template lang="html">
  <div class="">
    <layoutheader/>
    <v-content>
      <v-container>
        <v-layout row wrap>
         <span class="title text-capitalize">Welcome, {{account.user.name}}</span>
        </v-layout>
      <v-layout row wrap>
        <span  v-if="`${account.user.role}`== 700">(Admin User)</span>
        <span  v-if="`${account.user.role}`== 600">(Write & Read)</span>
        <span  v-if="`${account.user.role}`== 400">(Read Only)</span>
      </v-layout>
      <v-layout row wrap>
        <v-flex xs6 md4>
          <v-card class="item-card color-0">
            <v-container>
              <span v-if="content.items.content" class="white--text title">{{content.items.content.length}}&nbsp;Content Types</span>
                <span v-else class="white--text title" >0&nbsp;Content Types</span>
            </v-container>
          </v-card>
        </v-flex>
        <v-flex xs6 md4>
          <v-card class="item-card color-1">
            <v-container>
              <span v-if="item.items" class="white--text title">{{item.items.item.length}}&nbsp;Content Items</span>
              <span v-else class="white--text title" >0&nbsp;Content Items</span>
            </v-container>
          </v-card>
        </v-flex>
        <v-flex xs6 md4>
          <v-card class="item-card color-2">
            <v-container>
                <span v-if="users.all.items" class="white--text title">{{users.all.items.length}}&nbsp;Users</span>
                  <span v-else class="white--text title" >0&nbsp;Users</span>
            </v-container>
          </v-card>
        </v-flex>
        <v-flex xs6 md4>
          <v-card class="item-card color-3">
            <v-container>
              <span v-if="Object.keys(field.field).length>0" class="white--text title">{{ Object.keys(field.field).length}}&nbsp;Fields</span>
                <span v-else class="white--text title" >0&nbsp;Fields</span>
            </v-container>
          </v-card>
        </v-flex>
      </v-layout>
  </v-container>
  </v-content>
  </div>

</template>

<script>
/* eslint-disable*/
import { mapState, mapActions } from 'vuex'
import layoutheader from '@/components/LayoutHeader'
export default {
  components:{
    layoutheader
  },
  created(){
    const loggedIn = localStorage.getItem('user')
    if (!loggedIn) {
      this.$router.push('/login')
    }
},
methods:{
    ...mapActions('users', ['get_All']),
   ...mapActions('content', ['get_All']),
   ...mapActions('item', ['get_All']),
    ...mapActions('field', ['get_All']),
},
computed: {
  ...mapState({account: 'account', status: ['status'], user: ['user']}),
  ...mapState({users: 'users'}),
  ...mapState({content: 'content'}),
  ...mapState({item: 'item'}),
  ...mapState({field: 'field'}),
},
mounted(){
    this.get_All()
}
}
</script>

<style lang="css">
.item-card{
  margin: 12px;
}
.color-0{
  background: #8E2DE2;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #4A00E0, #8E2DE2);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #4A00E0, #8E2DE2); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

}
.color-1{
  background: #FF512F;  /* fallback for old browsers */
background: -webkit-linear-gradient(to right, #F09819, #FF512F);  /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to right, #F09819, #FF512F); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

}
.color-2{
  background: #FF416C;  /* fallback for old browsers */
background: -webkit-linear-gradient(to top, #FF4B2B, #FF416C);  /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to top, #FF4B2B, #FF416C); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

}
.color-3{
  background: #396afc;  /* fallback for old browsers */
background: -webkit-linear-gradient(to right, #2948ff, #396afc);  /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to right, #2948ff, #396afc); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
</style>
