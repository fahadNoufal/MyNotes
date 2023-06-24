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
