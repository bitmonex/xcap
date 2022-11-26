<template>
	<div class="load hide"><i class="bb"></i><b>xcap</b></div>
</template>

<script>
//лоадер

</script>

<style>
	/*Loading*/
	.load{
	  position:fixed; top:0; right:0; left:0; bottom:0;
	  z-index:99999;
	  background: rgba(0, 0, 0, 0.9);
	  z-index: 999999;
	  backdrop-filter: blur(5px);
	  -webkit-backdrop-filter: blur(5px);
	}
	.load b{
	  position:fixed;
	  top:50%;
	  left:50%;
	  transform:translateX(-50%) translateY(-50%);
	}
	.load b{color:#fff; font-size:1.6em; text-transform:uppercase; margin-top:135px;}
	.bb::before, .bb::after, .bb {
	  position: absolute;
	  z-index:999999;
	  top: 0;
	  bottom: 0;
	  left: 0;
	  right: 0;
	}
	.bb {
	  width: 200px;
	  height: 200px;
	  margin: auto;
	  background: url("@/assets/logo.png") no-repeat 50%/70% rgba(0, 0, 0, 0.1);
	  color: #c6ff00;
	  box-shadow: inset 0 0 0 1px #777;
	}
	.bb::before, .bb::after {
	  content: "";
	  z-index: -1;
	  margin: -5%;
	  box-shadow: inset 0 0 0 2px;
	  animation: clipMe 8s linear infinite;
	}
	.bb::before {animation-delay: -4s;}
	@keyframes clipMe{0%, 100%{clip: rect(0px, 220px, 2px, 0px);}25%{clip: rect(0px, 2px, 220px, 0px);}50%{clip: rect(218px, 220px, 220px, 0px);}75%{clip: rect(0px, 220px, 220px, 218px);}}
	*,*::before,*::after {box-sizing: border-box;}
</style>