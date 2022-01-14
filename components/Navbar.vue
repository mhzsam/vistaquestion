<template >
  <header>
    <nav>
      <ul class="nav_links">
        <li> <nuxt-link to="/question">تست</nuxt-link></li>
        
      </ul>
    </nav>
    <a  href="https://vista.ir" ><img class="logo" src="img/logo.png" alt=""  /></a>
    
  </header>
</template>
<script>
export default {
  name: "Navbar",
};
</script>
<style scoped>
*{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    background-color:#5e5d5d ;
    direction: rtl;
}

li ,a{
    font-weight: 500;
    font-size: 16px;
    color: white;
    text-decoration: none;
}
header{
    display: flex;
    justify-content:space-between ;
    align-items: center;
    padding: 10px 10%;
}
.logo{
    cursor: pointer;
    width: 50px;
}
.nav_links{
    list-style: none;
}
.nav_links li{
    display: inline-block;
    padding: 0px 20px;
}
.nav_links li a{
    transition: all 0.3s ease 0s;
}
.nav_links li a:hover{
   color: #0088a9;
}

</style>