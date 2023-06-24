```jsx

//installation
>>  npm install react-router-dom@6

// in App.js file 

import {BrowserRouter, Routes, Route,Link,NavLink} from 'react-router-dom'

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

- BrowserRouter is a component which wraps the entire application and allows us to use the router inside it.
- Routes and Route allows us to setup routes
- links is used to create links b/w different pages