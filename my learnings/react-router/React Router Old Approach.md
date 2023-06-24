```jsx

//installation

npm install react-router@6.4

import {
	createBrowserRouter,
	createRoutesFromElements,
	Routes, 
	Route,
	Link,
	NavLink,
	RouterProvider,
} from 'react-router-dom'


function App(){
	return(
		<BrowserRouter>
			<Routes>
				<Route path='/' element={<Home/>} />
				// path shows the url path and element shows the  jsx element to be displayed
				<Route path='/about' element={<About/>} />
				
			</Routes>
		</BrowserRouter>
	)
}

function Home(){
	return(
		<div>
			<h1>Hello</h1>
			<link to='/' index > Home </Link>
			// to='/' is same as specifying 'index'
			<Navlink to='about'> About </NavLink>
			//in navlink you can style the link if active (your 
			link gets a class of active when it is active)
		
			
		</div>
	)
}

```
