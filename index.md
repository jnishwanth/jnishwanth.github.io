## Delta WebDev Task1

Click [here](jnishwanth.github.io/HTML.html) to acess the webpage

The code for the file is given below

###HTML
```
<!DOCTYPE html>
<html>
	<link rel="stylesheet" type="text/css" href="CSS.css">
	<script type= "text/javascript" src="JS.js"></script>
<head>
	<title>Work</title>

</head>
  
<body>

	<div id="maindiv" class="num_container"></div>
	
	<button id="start" onclick="startgame();" class="general">START</button>

	<div id="timediv" class="general">0.000</div>

	<div id="besttime" class="general"></div>

	

</body>

</html>
```
###CSS
```
.num_container	{
	position: fixed;
	left: 50%;
	top: 50%;
	transform: translate(-50%,-50%);
	grid-template-columns: auto auto auto auto auto;
	display: grid;
	width: 505px;
	text-align: center;
	background-color: blue;
	border-radius: 9px;
	padding: 50px;
}
.num_button	{
	display: grid;
	text-align: center;
	background-color: red;
	display: table-cell;
	vertical-align: middle;
	font-size: 55px;
	border-radius: 6px;
	margin: 1px;
	width: 100px;
	height: 100px;
}

.general	{
	float: left;
	font-size: 30px;
}
```

###JS
```
var ASDF = 0;

//StartGame
function startgame(){
	ASDF++;
	var startbutton = document.getElementById('start');
	startbutton.innerHTML="RESET";
	if(ASDF>=2){location.reload();}
	//Best time
	var besttime= document.getElementById('besttime');
	if (localStorage.length==0) {besttime.innerHTML = "NONE";}
	else {
		var tmparr = JSON.parse(localStorage.getItem("best"));
		besttime.innerHTML = temparr[0];
	}

	/*function countdownpush(){
		setTimeout(function(){maindiv.appendChild(countdowndiv);},1000)
		maindiv.removeChild(maindiv.childNodes[0]);
		maindiv.removeChild(maindiv.childNodes[0]);
	}
	var coutdowndiv = document.createElement("div");
	countdowndiv.innerHTML = 3;
	countdownpush();
	countdowndiv.innerHTML = 2;
	countdownpush();
	countdowndiv.innerHTML = 1;
	countdownpush();*/



	//Random set generation
	var set = [];
	var randset = [];
	var r;
	for(let i=1; i<=25; ++i){
		set.push(i);
	}
	for(let i=1; i<=25; ++i){
		r = Math.floor(Math.random()*(26-i));
    	randset.push(set[r]);
    	set.splice(r,1);
	}

	//Button creation
	var maindiv = document.getElementById('maindiv');
	for(let i=1; i<=25; ++i){ 
		var numbtn = document.createElement('button');
   		numbtn.setAttribute('class','num_button');
   		numbtn.innerHTML = randset[i-1];
   		numbtn.setAttribute('onclick','checknum(this);');
  	 	maindiv.appendChild(numbtn);
	}

	var count = 1;
	var time=0.000;
	//Timer
	/*var timediv = document.findElementById('timediv');

	function timeinc(){
		time=time+0.001;
		timediv.innerHTML=time;
	}

	while(count<51){
	setTimeout(timeinc(),1);
	}*/

	//onclick

	function checknum(clickedbtn){
		if (clickedbtn.innerHTML == count){
			if (count<=25){
					++count;
					clickedbtn.innerHTML = 25 + parseInt(clickedbtn.innerHTML);
				}
			else{
				++count;
				clickedbtn.innerHTML="";
			}
		}			
		//if (count > 50){
			//endfun();
		//}
	}

	/*function endfun(){
		
		if (localStorage.length==0) {
			var bestarr = [];
			bestarr.push(time);
			localStorage.setItem("best", JSON.stringify(bestarr));
		}
		var bestarr = JSON.parse(localStorage.getItem("best"));
		if (time<bestarr[0])	{bestarr.splice(0,0,time)}
		if ( (time>bestarr[0]) && (time<bestarr[1]) )	{bestarr.splice(1,0,time)}
		if ( (time>bestarr[1]) && (time<bestarr[2]) )	{bestarr.splice(2,0,time)}
		if ( (time>bestarr[2]) && (time<bestarr[3]) )	{bestarr.splice(3,0,time)}
		if ( (time>bestarr[3]) && (time<bestarr[4]) )	{bestarr.splice(4,0,time)}
		localStorage.setItem("best", JSON.stringify(bestarr));
		location.reload();
	}*/
}
```
