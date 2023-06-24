
![[Pasted image 20230503235441.png]]
	
```js
gsap.to('.box',{
	x:0,
	scrollTrigger:{
		trigger:'.box1',
		// animation is triggered when the trigger element reaches the start
		start:'20px 80%',
		// these values like 20px or % are always relative to top of the screen
		end:'+=300',
		// here we measures the end of animation in relation to the start , ie, after 300px from where it have started
		// we can also use functions to set the strt/end of the scroll trigger if you have a responsive fancy css box
		end:()=> '+=' + document.querySelector('.c').offsetWidth,
		markers:true,
		id:'marker-name',//this will help when you have multiple scroll triggers to identify specific st
		// you can also use a different elements position to end the animation of element (".box") . ie:
		endTrigger:'.c',
		end:'bottom 80%',
		// here , the animation ends when the '.c' element reaches its end point
		scrub:3, // seconds to catch up scrool scrub
		pin:true, // we could also use other elements '.box3'
		//pinns the element to the screen where it was at the starrt of the screen when the scrool trigger is active  ie, from start to end
		 pinSpacing:false,
		//by default st adds padding at the bottom of the element in order for the element below it to catch up, so that they dont overlap each other
		// by setting 'pinSpacing:false' they overlap
		onEnter:()=>{...},
		onLeave:()=>{...},
		onEnterBack:()=>{...},
		onLeaveBack:()=>{...},
		onUpdate:(self)=>{console.log(self.progress.toFixed(3)},
		// self.progress gives a numer based on the scroll trigger progress b/w 0 and 1. toFixed(3) sets it to 3 decimal places 
		onToggle:(self)=>{self.isActive},
		//runs everytime the when the scrolltrigger becomes active or not (when changes its value)
		toggleClass:'blue',
		//toggles this class when st is active and 
		
		//function callbacks
		scroller:'.parent-container',
		
		>>> |Use it inside a useEffect|
		// t's the thing whose scrollbar is linked to the ScrollTrigger. By default, it's the window (viewport).
	}

// You can also use scrolltrigger inside timeline to make the timeline actions based on scroll scrub
let tl= gsap.timeline({scrollTrigger:{....}})

})
```

## Creating scrolltrigger intipentendly

```js
// you can also create a scrolltrigger  intipentently
ScrollTrigger.create({
	animation:timeL,//pass in an animation like tl or tween
	trigger:'.box-2',
	.....
})
```

## Default scrollTrigger settings

```js
ScrollTrigger.defaults({
	toggleActions:"restart pause resume none",
	markers:true,
})
// used when you have to set default st properties
```

## To dynamically change scroll trigger position

```js
onComplete:()=>{ScrollTrigger.refresh();},
```

## To solve pin spacing react problem
```js
useEffect(() => {
	gsap.registerPlugin(ScrollTrigger);
	gsap.to('.c3', {
		opacity: 0.5,
		scrollTrigger: {
		trigger: '.c3',
		markers: true,
		start: 'top center',
		end: 'top 100px',
		scrub: true,
		pin: true,
		},
	});
	return () => {
		ScrollTrigger.getAll().forEach((instance) => {
		instance.kill()  });
		};
}, []);
```

