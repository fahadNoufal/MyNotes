# Installation
![[Pasted image 20230503235052.png]]

## .to  .from  .fromTo and .set

```js
	// "to" tween (animate to provided values)  
	tween=gsap.to(".selector", 
		{// selector text, Array, or object  
	x: 100, // any properties (not limited to CSS)  
	backgroundColor: "red", // camelCase  
	duration: 1, // seconds  
	delay: 0.5,  
	ease: "power2.inOut",
	stagger: 0.1, // stagger start times 
	paused: true, // default is false 
	overwrite: "auto", // default is false  
	repeat: 2, // number of repeats (-1 for infinite)  
	repeatDelay: 1, // seconds between repeats  
	repeatRefresh: true, // invalidates on each repeat  
	yoyo: true, // if true > A-B-B-A, if false > A-B-A-B  
	yoyoEase: true, // or ease like "power2"  i
	mmediateRender: false,  
	onComplete: myFunc,  
	// other callbacks:   
	// onStart, onUpdate, onRepeat, onReverseComplete  
	// Each callback has a params property as well  
	// i.e. onUpdateParams (Array)  
	});
```

#### .kill()
```js
button.addEventListener('click',(e)= >{
	tween.kill()
})
```
>	this wil kill the animation and make it like it was paused. The element's still or position will be same as when it was killed
>	- style not removed

#### .revert()
`tween.revert()`
>	this will make the animated element go back to its orginal place before the animation
>	- animation is killed , style removed , reverted to pre-animation state

#### .context()
	It will be really defficult to keep track of every element that need to be reverted all at once as the no of elements that needs to be reverted increases: for that we use .context()
	
```js
	let ctx= gsap.context(()=>{
		// Then drop all the animations that needs to be reverted all at once
		// animations can be anything like tweens,timeline,scrolt 
		let tweenOne=gsap.to('.one',{...changes})
		let tweenTwo=gsap.to('.two',{...changes})
		let tweenThree=gsap.to('.three',{...changes})
		tl.
	})
	btn.addEventListener('click',(e)=>{ctx.revert})
```

gsap.to(".selector", { [duration: 1](https://greensock.com/docs/v3/GSAP/Tween/duration()),   [delay: 0.5](https://greensock.com/docs/v3/GSAP/Tween/delay()),  [ease: "power2.inOut",](https://greensock.com/docs/v3/Eases)  [stagger: 0.1](https://greensock.com/docs/v3/Staggers),  [paused: true](https://greensock.com/docs/v3/GSAP/Tween/paused()),  [repeat: 2](https://greensock.com/docs/v3/GSAP/Tween/repeat())  [repeatDelay: 1](https://greensock.com/docs/v3/GSAP/Tween/repeatDelay()) [yoyo: true](https://greensock.com/docs/v3/GSAP/Tween/yoyo())

```js
// "from" tween (animate from provided values)  
gsap.from(".selector", {fromVars});


// "fromTo" tween (define both start and end values)  
gsap.fromTo(".selector", {fromVars}, {toVars});
// special properties (duration, ease, etc.) go in toVars


// set values immediately (no animation)  
gsap.set(".selector", {toVars});
```


# Timelines

	![[Pasted image 20230503234818.png]]

## Sequence multiple tweens
![[Pasted image 20230503234851.png]]

# Position
![[Pasted image 20230503234942.png]]

# Control methods
![[Pasted image 20230503235322.png]]

# Scrolltriggers

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
		// t's the thing whose scrollbar is linked to the ScrollTrigger. By default, it's the window (viewport).
	}

// You can also use scrolltrigger inside timeline to make the timeline actions based on scroll scrub
let tl= gsap.timeline({scrollTrigger:{....}})

// you can also create a scrolltrigger  intipentently
ScrollTrigger.create({
	animation:timeL,//pass in an animation like tl or tween
	trigger:'.box-2',
	.....
})
ScrollTrigger.defaults({
	toggleActions:"restart pause resume none",
	markers:true,
})
// used when you have to set default st properties
})
```