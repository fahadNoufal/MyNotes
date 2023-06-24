`gsap.registerPlugin(MotionPathPlugin)`

```js
gsap.to('.moving-item',{
	duration:5,
	motionPath:{
		path:'#path',//to move in the specified path (we can also provide an svg path)
		path:[{x:100,y:100},{x:300,y:300}] ,
		curviness:0 , // 0 means no curve , 2 means over curve
		//travel through co-ordinates(nice curved motion occurs through these points) 
		align:'#path',// to move along the specified path
		align:'self', // moves right from where the item sits
		autoRotate:true,
		start:0.25, // starts from 25% of the path
		end:1.25, // ends after 125% of the actual path
	}
})

//to move through the middle of the path
gsap.set('.moving-item',{
	xPercent:-50,
	yPercent:-50,
	transformOrigin:'50% 50%'
})
```