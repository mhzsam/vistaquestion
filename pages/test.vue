<template>
<div>
<div class="triangle-up hovercolor"><span class="line1"></span></div>
<div  class="trapezoid1 hovercolor"><span class="line2"></span></div>
<div  class="trapezoid2 hovercolor"><span class="line3"></span></div>
<div  class="trapezoid3 hovercolor"><span class="line4"></span></div>

</div>
</template>

<script>
export default {
  name: "test",
};
</script>
<style scoped>
.line1{
  position: absolute;
  top:50px;

  background-color: brown;
  height: 5px;
  width: 250px;
  z-index: -9999;
}
.line2{
  position: absolute;
  top:50px;

  background-color: brown;
  height: 5px;
  width: 300px;
  z-index: -9999;
}
.line3{
  position: absolute;
  top:50px;

  background-color: brown;
  height: 5px;
  width: 350px;
  z-index: -9999;
}
.line4{
  position: absolute;
  top:50px;

  background-color: brown;
  height: 5px;
  width: 400px;
  z-index: -9999;
}
.triangle-up {
  position: relative;
  margin: auto;
	width: 0;
	height: 0;
	border-left: 50px solid transparent;
	border-right: 50px solid transparent;
	border-bottom: 100px solid rgb(11, 224, 107);
}

.trapezoid1{
  position: relative;
  margin: auto;
  	width: 200px;
	height: 0;
	border-left: 50px solid transparent;
	border-right: 50px solid transparent;
	border-bottom: 100px solid rgb(11, 224, 107);
}
.trapezoid2{
  position: relative;
  margin: auto;
  	width: 300px;
	height: 0;
	border-left: 50px solid transparent;
	border-right: 50px solid transparent;
	border-bottom: 100px solid rgb(11, 224, 107);
}
.trapezoid3{
  position: relative;
  margin: auto;
  	width: 400px;
	height: 0;
	border-left: 50px solid transparent;
	border-right: 50px solid transparent;
	border-bottom: 100px solid rgb(11, 224, 107);
}
.hovercolor:hover{
  border-bottom-color: aqua;
 
}
</style>
