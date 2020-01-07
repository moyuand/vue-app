<template>
  <div class="user">
    <div class="header">
      <div class="photo">
        <img src="../../assets/user1.png" alt=""/>
      </div>
      <div class="name">{{info.name}}</div>
    </div>
    <van-cell title="常用地址" is-link to="/manager/address" icon="location-o"/>
    <van-cell title="所有订单" is-link to="/manager/order" icon="balance-list-o"/>
    <van-cell title="常用联系人" is-link to="/manager/contact" icon="contact"/>
    <van-panel title="余额" desc="" status="请充值">
      <div>00.00元</div><center><van-button type="info">充值</van-button></center>
    </van-panel>
    <div class="btn" @click="logoutHandler">
      退出
    </div>
  </div>
</template>
<script>
import {mapState, mapActions} from 'vuex'
export default {
  methods:{
    ...mapActions('user',['logout']),
    toAddressHandler(){
      // this.$router.push({path:'/manager/address'})
    },
    logoutHandler(){
      this.logout()
      .then(()=>{
        this.$router.push({path:'/login'})
      })
    }
  },
  computed:{
    ...mapState("user",["info"])
  }
}
</script>

<style scoped>
.header {
  padding-top: 46px;
  text-align: center;
  background: #1659a0;
  margin-bottom: 2em;
}

.header .photo {
  margin: 0 auto;
  width: 10em;
  height: 10em;
  border-radius: 50%;
  box-sizing: border-box;
  border:1px solid #1659a0;
  overflow:hidden;
  padding: 1em;
}
.header .name {
  line-height: 3em;
  font-size: 16px;
  color: #ffffff;

}
.header .photo img {
 width: 100%;
 border-radius: 50%;
}

.btn {
  width: 90%;
  margin: 0 auto;
  line-height: 3em;
  text-align: center;
  border: 1px solid #ededed;
  border-radius: 1.5em;
}

</style>