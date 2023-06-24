These loaders loads and fetches the data before the components loads 

```jsx

import {careersLoader} from './careers'

const router=createBrowserRouter(
	createRoutesFromElements(
		<Route>
			<Route index element={<Home/>} />
			<Route path='about' element={<About/>} />
			<Route path='help' element={<Help/>}>
				<Route path='faq' element={<Faq/>} />
				<Route path='chat' element={<Chat/>} />
			</Route>
			
			>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
			
			<Route path='careers' element={<CareerLayout/>}>
				<Route 
					index 
					element={<Careers/>} 
					loader={careersLoader}
				/>
			</Route>
			
			>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
			
			<Route path='*' element={<ErrorPageElement/>} />
			//this route will be matched if all the above url 
				dosenot match
		</Route>
	)
)

```

in Careers.js
```jsx
import useLoaderData from 'react-router-dom'

export default const Careers=()=>{ 
	const data= useLoaderData()
	// this will return the resolved data
	return(
		.......
	)
}

//loader function
export const careersLoader=async()=>{
	const res= await fetch('https://anywebsite.com')
	return res.json()
	//this return is a promis, but we dont have to worry about that, react -router will take care of that and resolve it.
	//later we can use it inside this component
}

```
