<template>
  <div id="app">
    <div class="page4">
      <div class="header">
        <div class="nav">
          <a href='index.html'> Форма </a>
          <a href='about.html'> Превью </a>
        </div>
      </div>
      <div class="main">
        <UserListCreator/>
      </div>
      <div class="footer">
        <p id='copyright'>All rights reserved</p>
      </div>
    </div>
    <!-- <UserListCreator/> -->
    <!-- <UserDataList/> -->
    
    
  </div>
</template>

<script>

import UserListCreator from '@/components/UserListCreator.vue'

export default {
  name: 'About',
  components: {
    UserListCreator
  }
}
</script>

<style>
.page4 {
  position: relative;
  width: 1366px;
  height: 868px;  

  font-family: Arial, Helvetica, sans-serif;
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    line-height: 24px;
}


.header{
  position: absolute;
  width: 1366px;
  height: 76px;
  left: 0px;
  top: 0px;
}

.nav {
  flex-direction: row;
  position: absolute;
  width: 135px;
  height: 70px;
  right: 574px;
  top: 7px;

}

.footer {
  position: absolute;
  width: 1366px;
  height: 76px;
  left: 0px;
  top: 792px;
  background: #FAFAFA;

}

#copyright {
display: flex;
flex-direction: row;
align-items: center;
padding: 0px;

position: absolute;
width: 116px;
height: 16px;
left: 625px;
top: 30px;

font-style: normal;
font-weight: normal;
font-size: 13px;
line-height: 16px;

}

a {
  color: rgba(17, 17, 17, 0.48);
  text-decoration: none;
}
</style>
