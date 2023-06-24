	A `gsap.context()` offers two key benefits:

-   **Collects all GSAP animations and ScrollTriggers** that are created within the supplied function so that you can easily `revert()` or `kill()` **ALL** of them at once. No need to keep track of a bunch of variables, Arrays, etc.  

	  `This is particularly useful in React modules or anywhere you need to be able to "clean up" by reverting elements to their original state.`

-  **Scopes all selector text to a particular Element or Ref**. This can help simplify your code quite a bit and avoid needing to create lots of `refs` in React/Angular. Any GSAP-related selector text inside the supplied function will only apply to descendants of the Element/Ref.


## Revert all at once

Let's say you've got a **big** block of GSAP code that's creating a bunch of different animations and you need to be able to `revert()` them all...

```js
let ctx = gsap.context(() => {
 gsap.to(...);
 gsap.from(...);
 gsap.timeline().to(...).to(...);
 ...
 // then later...
 ctx.revert(); // BOOM! Every GSAP animation created in that   function gets reverted!
});
```

## Scoping selector text

No more creating a Ref for every element you want to animate!

```js
let ctx = gsap.context(() => {
  gsap.to(".box", {...}) // <- normal selector text, automatically scoped to myRefOrElement
  gsap.from(".circle", {...}); 
  
}, myRefOrElement); // <- scope!!!
```

The `scope` can be selector text itself like ".myClass", or an Element, React Ref or Angular ElementRef.



```js
let ctx = gsap.context((context) => {
  // use any arbitrary string as a name; it'll be added to the Context object, so in this case you can call ctx.onClick() later...
	
  // Here we name the context 'onClick' , it is not a class
  context.add("onClick", (e) => {
    gsap.to(...); // <-- gets added to the Context!
  });
}, myRefOrElement);
// now the Context has an onClick() method we can tap into and any animations in that function will get added to the Context
myButton.addEventListener("click", (e) => ctx.onClick(e));

//Now if we call ctx.revert(), it ('onClick') will not revert . 
// it will only revert if we call ctx.onclick(e) , like we saw above
```


 you can directly add things to the Context **immediately** like this (function as the first parameter):

```js
// create context
let ctx = gsap.context(() => {...});
// then later, add to it:
ctx.add(() => {
  gsap.to(...); // now all these get added to the Context.
  gsap.from(...); 
});
```

## Cleanup function

You can optionally return a "cleanup function" that should be called if/when the context gets reverted. This can contain your own custom cleanup code:
```js
let ctx = gsap.context(() => {
  ...
  return () => {
    // my custom cleanup code. Called when ctx.revert() is triggered. 
    };
});
```
You can return a clean up function in any `.add()` function too; They'll all get called when the Context's `revert()` is invoked.

## Ignoring certain animations/ScrollTriggers

In very uncommon situations, you may want to create certain GSAP animations and/or ScrollTriggers inside the function that should be **excluded from the Context** (not reverted/killed when the Context gets reverted/killed) in which case you can use an `ignore()` like this:

```js
let ctx = gsap.context((self) => {
  gsap.to(...); // <- will get reverted when ctx.revert() is called
  self.ignore(() => {
    gsap.to(...); // <- will NOT get reverted when ctx.revert() is called. Ignored, not recorded in the Context.
  })
})
```

## Notes :
![[Pasted image 20230514122355.png]]

