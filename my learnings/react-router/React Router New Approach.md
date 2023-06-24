
```jsx

npm install react-router-dom@6.4

import {
	createBrowserRouter,
	createRoutesFromElements,
	Route,
	NavLink,
	RouterProvider,
	Outlet,
} from 'react-router-dom'

const Navbar=()=(
	<nav>
		<h1>Hello world</h1>
		<NavLink to = "/" >Home</NavLink>
		<NavLink to = "about">About</NavLink>
		<div>
			<Outlet/>
		</div>
	</nav>
)

const router=createBrowserRouter(
	createRoutesFromElements(
		<Route>
			<Route index element={<Home/>} />
			<Route path='about' element={<About/>} />
			<Route path='help' element={<Help/>}>
				<Route path='faq' element={<Faq/>} />
				<Route path='chat' element={<Chat/>} />
			</Route>
			
			<Route path='*' element={<ErrorPageElement/>} />
			//this route will be matched if all the above url 
				dosenot match
		</Route>
	)
)
// all these thing like navlink, link route will only work inside the scope of RouterProvider

function App(){
	return(
		<RouterProvider router={router} />
	)
}


```


- in navlink you just have to provide the relative path in path =''
  > ie, if you ar in `<Help/>` component you just have to provide 
  > `<Navlink to='faq'>` instead of the whole path `.../help/faq`
  
