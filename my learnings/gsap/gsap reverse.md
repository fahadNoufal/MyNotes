```js
let tl=useRef()
useEffect(()=>{
	let ctx=gsap.context(()=>{
	tl.current = gsap.timeline({paused:true});	
	tl.current.to('.class',{
		duration:0.7,
		scale: 0.84,
		x: "65%",
		.....
	})
	tl.current.from(....);
	tl.current.fromTo(...)

	return ()=>{ctx.revert()}
},[])

useEffect(()=>{
	showMenu?tl.current.play():tl.current.reverse()
},[showMenu])
```