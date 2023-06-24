```js
let tl=useRef()
useEffect(()=>{
	let ctx=gsap.context(()=>{
	// you have to assign tl.current inside useEffect
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

```js
let tl=useRef()
const dispatch =useDispatch()
function handleTaskCreation(){
	tl.current=gsap.timeline()
	tl.current.to('.task-creation-container',{
		y:'0',
		ease:'back.out(0.3)',
		duration:0.5,
	})
	tl.current.to('.black-filter',{
		height:0,
		duration:0.3,
		ease:'power3.out'
	})
	tl.current.to('.taskCreate-fields',{
		y:0,
		opacity:1,
		duration:0.5,
		ease:'power3.out'
	})
} 
function handleCloseTaskCreation(){
	tl.current.pause()
	tl.current.reverse()
}
```