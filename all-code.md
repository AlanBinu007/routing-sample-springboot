<!---
Current Directory : /in28Minutes/git/spring-boot-react-fullstack-examples/spring-boot-react-hello-world-with-routing
-->

## Complete Code Example


### /frontend-spring-boot-react-hello-world-with-routing/public/index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <meta name="theme-color" content="#000000" />
    <!--
      manifest.json provides metadata used when your web app is installed on a
      user's mobile device or desktop. See https://developers.google.com/web/fundamentals/web-app-manifest/
    -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <!--
      Notice the use of %PUBLIC_URL% in the tags above.
      It will be replaced with the URL of the `public` folder during the build.
      Only files inside the `public` folder can be referenced from the HTML.

      Unlike "/favicon.ico" or "favicon.ico", "%PUBLIC_URL%/favicon.ico" will
      work correctly both with client-side routing and a non-root public URL.
      Learn how to configure a non-root public URL by running `npm run build`.
    -->
    <title>React App</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->
  </body>
</html>
```
---

### /frontend-spring-boot-react-hello-world-with-routing/public/manifest.json

```json
{
  "short_name": "React App",
  "name": "Create React App Sample",
  "icons": [
    {
      "src": "favicon.ico",
      "sizes": "64x64 32x32 24x24 16x16",
      "type": "image/x-icon"
    }
  ],
  "start_url": ".",
  "display": "standalone",
  "theme_color": "#000000",
  "background_color": "#ffffff"
}
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/App.css

```css
@import url(https://unpkg.com/bootstrap@4.1.0/dist/css/bootstrap.min.css)
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/index.js

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/component/MenuComponent.js

```js
import React, { Component } from 'react';
import { Link } from 'react-router-dom'

class MenuComponent extends Component {
    componentDidMount() {

    }
    render() {
        return (
            <header>
                <nav className="navbar navbar-expand-md navbar-dark bg-dark">
                    <div><a href="http://www.in28minutes.com" className="navbar-brand">in28Minutes</a></div>
                    <ul className="navbar-nav">
                        <li><Link className="nav-link" to="/hello-world-string">Hello World String</Link></li>
                        <li><Link className="nav-link" to="/hello-world-bean">Hello World Bean</Link></li>
                    </ul>
                </nav>
            </header>
        )

    }

}

export default MenuComponent
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/component/HelloWorldBeanComponent.js

```js
import React, { Component } from 'react';
import HelloWorldService from '../service/HelloWorldService';

class HelloWorldBeanComponent extends Component {
    constructor(props) {
        super(props)
        this.state = {
            welcomeMessage: ''
        }
    }

    componentDidMount() {
        HelloWorldService.executeHelloWorldBeanService()
            .then(response => this.setState({ welcomeMessage: response.data.message }))
            .catch(this.setState({ welcomeMessage: 'Error Processing Request' }))
    }

    render() {
        return (<>
            <h1>Hello World String Component</h1>
            <div className="container">
                {this.state.welcomeMessage}
            </div>
            <div className="row">
                <button className="btn btn-success" onClick={this.gotoStringComponent}>Go Back</button>
            </div>
        </>
        )
    }

    gotoStringComponent = () => {
        this.props.history.push('/hello-world-string')
    }
}

export default HelloWorldBeanComponent
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/component/HelloWorldApp.js

```js
import React, { Component } from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom'
import MenuComponent from './MenuComponent'
import HelloWorldBeanComponent from './HelloWorldBeanComponent';
import HelloWorldStringComponent from './HelloWorldStringComponent';

class HelloWorldApp extends Component {
    render() {
        return (
            <>
                <Router>
                    <>
                        <MenuComponent />
                        <div className="container">
                            <Switch>
                                <Route path="/" exact component={HelloWorldStringComponent} />
                                <Route path="/hello-world-string" component={HelloWorldStringComponent} />
                                <Route path="/hello-world-bean" component={HelloWorldBeanComponent} />
                            </Switch>
                        </div>
                    </>
                </Router>
            </>
        )
    }
}

export default HelloWorldApp;
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/component/HelloWorldStringComponent.js

```js
import React, { Component } from 'react';
import HelloWorldService from '../service/HelloWorldService';

class HelloWorldStringComponent extends Component {
    constructor(props) {
        super(props)
        this.state = {
            welcomeMessage: ''
        }
    }

    componentDidMount() {
        HelloWorldService.executeHelloWorldService()
            .then(response => this.setState({ welcomeMessage: response.data }))
            .catch(this.setState({ welcomeMessage: 'Error Processing Request' }))
    }

    render() {
        return (<>
            <h1>Hello World String Component</h1>
            <div className="container">
                {this.state.welcomeMessage}
            </div>
            <div className="row">
                <button className="btn btn-success" onClick={this.gotoBeanComponent}>Go</button>
            </div>
        </>
        )
    }

    gotoBeanComponent = () => {
        this.props.history.push('/hello-world-bean')
    }
}

export default HelloWorldStringComponent
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/index.css

```css
body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
    "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
    monospace;
}
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/App.test.js

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

it('renders without crashing', () => {
  const div = document.createElement('div');
  ReactDOM.render(<App />, div);
  ReactDOM.unmountComponentAtNode(div);
});
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/serviceWorker.js

```js
// This optional code is used to register a service worker.
// register() is not called by default.

// This lets the app load faster on subsequent visits in production, and gives
// it offline capabilities. However, it also means that developers (and users)
// will only see deployed updates on subsequent visits to a page, after all the
// existing tabs open on the page have been closed, since previously cached
// resources are updated in the background.

// To learn more about the benefits of this model and instructions on how to
// opt-in, read https://bit.ly/CRA-PWA

const isLocalhost = Boolean(
  window.location.hostname === 'localhost' ||
    // [::1] is the IPv6 localhost address.
    window.location.hostname === '[::1]' ||
    // 127.0.0.1/8 is considered localhost for IPv4.
    window.location.hostname.match(
      /^127(?:\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)){3}$/
    )
);

export function register(config) {
  if (process.env.NODE_ENV === 'production' && 'serviceWorker' in navigator) {
    // The URL constructor is available in all browsers that support SW.
    const publicUrl = new URL(process.env.PUBLIC_URL, window.location.href);
    if (publicUrl.origin !== window.location.origin) {
      // Our service worker won't work if PUBLIC_URL is on a different origin
      // from what our page is served on. This might happen if a CDN is used to
      // serve assets; see https://github.com/facebook/create-react-app/issues/2374
      return;
    }

    window.addEventListener('load', () => {
      const swUrl = `${process.env.PUBLIC_URL}/service-worker.js`;

      if (isLocalhost) {
        // This is running on localhost. Let's check if a service worker still exists or not.
        checkValidServiceWorker(swUrl, config);

        // Add some additional logging to localhost, pointing developers to the
        // service worker/PWA documentation.
        navigator.serviceWorker.ready.then(() => {
          console.log(
            'This web app is being served cache-first by a service ' +
              'worker. To learn more, visit https://bit.ly/CRA-PWA'
          );
        });
      } else {
        // Is not localhost. Just register service worker
        registerValidSW(swUrl, config);
      }
    });
  }
}

function registerValidSW(swUrl, config) {
  navigator.serviceWorker
    .register(swUrl)
    .then(registration => {
      registration.onupdatefound = () => {
        const installingWorker = registration.installing;
        if (installingWorker == null) {
          return;
        }
        installingWorker.onstatechange = () => {
          if (installingWorker.state === 'installed') {
            if (navigator.serviceWorker.controller) {
              // At this point, the updated precached content has been fetched,
              // but the previous service worker will still serve the older
              // content until all client tabs are closed.
              console.log(
                'New content is available and will be used when all ' +
                  'tabs for this page are closed. See https://bit.ly/CRA-PWA.'
              );

              // Execute callback
              if (config && config.onUpdate) {
                config.onUpdate(registration);
              }
            } else {
              // At this point, everything has been precached.
              // It's the perfect time to display a
              // "Content is cached for offline use." message.
              console.log('Content is cached for offline use.');

              // Execute callback
              if (config && config.onSuccess) {
                config.onSuccess(registration);
              }
            }
          }
        };
      };
    })
    .catch(error => {
      console.error('Error during service worker registration:', error);
    });
}

function checkValidServiceWorker(swUrl, config) {
  // Check if the service worker can be found. If it can't reload the page.
  fetch(swUrl)
    .then(response => {
      // Ensure service worker exists, and that we really are getting a JS file.
      const contentType = response.headers.get('content-type');
      if (
        response.status === 404 ||
        (contentType != null && contentType.indexOf('javascript') === -1)
      ) {
        // No service worker found. Probably a different app. Reload the page.
        navigator.serviceWorker.ready.then(registration => {
          registration.unregister().then(() => {
            window.location.reload();
          });
        });
      } else {
        // Service worker found. Proceed as normal.
        registerValidSW(swUrl, config);
      }
    })
    .catch(() => {
      console.log(
        'No internet connection found. App is running in offline mode.'
      );
    });
}

export function unregister() {
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.ready.then(registration => {
      registration.unregister();
    });
  }
}
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/service/HelloWorldService.js

```js
import axios from 'axios'

class HelloWorldService {

    executeHelloWorldService() {
        return axios.get('http://localhost:8080/hello-world');
    }

    executeHelloWorldBeanService() {
        return axios.get('http://localhost:8080/hello-world-bean');
    }

    executeHelloWorldPathVariableService(name) {
        return axios.get(`http://localhost:8080/hello-world/path-variable/${name}`);
    }

}

export default new HelloWorldService()
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/logo.svg

```
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 841.9 595.3">
    <g fill="#61DAFB">
        <path d="M666.3 296.5c0-32.5-40.7-63.3-103.1-82.4 14.4-63.6 8-114.2-20.2-130.4-6.5-3.8-14.1-5.6-22.4-5.6v22.3c4.6 0 8.3.9 11.4 2.6 13.6 7.8 19.5 37.5 14.9 75.7-1.1 9.4-2.9 19.3-5.1 29.4-19.6-4.8-41-8.5-63.5-10.9-13.5-18.5-27.5-35.3-41.6-50 32.6-30.3 63.2-46.9 84-46.9V78c-27.5 0-63.5 19.6-99.9 53.6-36.4-33.8-72.4-53.2-99.9-53.2v22.3c20.7 0 51.4 16.5 84 46.6-14 14.7-28 31.4-41.3 49.9-22.6 2.4-44 6.1-63.6 11-2.3-10-4-19.7-5.2-29-4.7-38.2 1.1-67.9 14.6-75.8 3-1.8 6.9-2.6 11.5-2.6V78.5c-8.4 0-16 1.8-22.6 5.6-28.1 16.2-34.4 66.7-19.9 130.1-62.2 19.2-102.7 49.9-102.7 82.3 0 32.5 40.7 63.3 103.1 82.4-14.4 63.6-8 114.2 20.2 130.4 6.5 3.8 14.1 5.6 22.5 5.6 27.5 0 63.5-19.6 99.9-53.6 36.4 33.8 72.4 53.2 99.9 53.2 8.4 0 16-1.8 22.6-5.6 28.1-16.2 34.4-66.7 19.9-130.1 62-19.1 102.5-49.9 102.5-82.3zm-130.2-66.7c-3.7 12.9-8.3 26.2-13.5 39.5-4.1-8-8.4-16-13.1-24-4.6-8-9.5-15.8-14.4-23.4 14.2 2.1 27.9 4.7 41 7.9zm-45.8 106.5c-7.8 13.5-15.8 26.3-24.1 38.2-14.9 1.3-30 2-45.2 2-15.1 0-30.2-.7-45-1.9-8.3-11.9-16.4-24.6-24.2-38-7.6-13.1-14.5-26.4-20.8-39.8 6.2-13.4 13.2-26.8 20.7-39.9 7.8-13.5 15.8-26.3 24.1-38.2 14.9-1.3 30-2 45.2-2 15.1 0 30.2.7 45 1.9 8.3 11.9 16.4 24.6 24.2 38 7.6 13.1 14.5 26.4 20.8 39.8-6.3 13.4-13.2 26.8-20.7 39.9zm32.3-13c5.4 13.4 10 26.8 13.8 39.8-13.1 3.2-26.9 5.9-41.2 8 4.9-7.7 9.8-15.6 14.4-23.7 4.6-8 8.9-16.1 13-24.1zM421.2 430c-9.3-9.6-18.6-20.3-27.8-32 9 .4 18.2.7 27.5.7 9.4 0 18.7-.2 27.8-.7-9 11.7-18.3 22.4-27.5 32zm-74.4-58.9c-14.2-2.1-27.9-4.7-41-7.9 3.7-12.9 8.3-26.2 13.5-39.5 4.1 8 8.4 16 13.1 24 4.7 8 9.5 15.8 14.4 23.4zM420.7 163c9.3 9.6 18.6 20.3 27.8 32-9-.4-18.2-.7-27.5-.7-9.4 0-18.7.2-27.8.7 9-11.7 18.3-22.4 27.5-32zm-74 58.9c-4.9 7.7-9.8 15.6-14.4 23.7-4.6 8-8.9 16-13 24-5.4-13.4-10-26.8-13.8-39.8 13.1-3.1 26.9-5.8 41.2-7.9zm-90.5 125.2c-35.4-15.1-58.3-34.9-58.3-50.6 0-15.7 22.9-35.6 58.3-50.6 8.6-3.7 18-7 27.7-10.1 5.7 19.6 13.2 40 22.5 60.9-9.2 20.8-16.6 41.1-22.2 60.6-9.9-3.1-19.3-6.5-28-10.2zM310 490c-13.6-7.8-19.5-37.5-14.9-75.7 1.1-9.4 2.9-19.3 5.1-29.4 19.6 4.8 41 8.5 63.5 10.9 13.5 18.5 27.5 35.3 41.6 50-32.6 30.3-63.2 46.9-84 46.9-4.5-.1-8.3-1-11.3-2.7zm237.2-76.2c4.7 38.2-1.1 67.9-14.6 75.8-3 1.8-6.9 2.6-11.5 2.6-20.7 0-51.4-16.5-84-46.6 14-14.7 28-31.4 41.3-49.9 22.6-2.4 44-6.1 63.6-11 2.3 10.1 4.1 19.8 5.2 29.1zm38.5-66.7c-8.6 3.7-18 7-27.7 10.1-5.7-19.6-13.2-40-22.5-60.9 9.2-20.8 16.6-41.1 22.2-60.6 9.9 3.1 19.3 6.5 28.1 10.2 35.4 15.1 58.3 34.9 58.3 50.6-.1 15.7-23 35.6-58.4 50.6zM320.8 78.4z"/>
        <circle cx="420.9" cy="296.5" r="45.7"/>
        <path d="M520.5 78.1z"/>
    </g>
</svg>
```
---

### /frontend-spring-boot-react-hello-world-with-routing/src/App.js

```js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';
import HelloWorldApp from './component/HelloWorldApp';

class App extends Component {
  render() {
    return (
      <div className="App">
        <HelloWorldApp />
      </div>
    );
  }
}

export default App;
```
---

### /frontend-spring-boot-react-hello-world-with-routing/package.json

```json
{
  "name": "spring-boot-react-hello-world-with-routing",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "axios": "^0.18.0",
    "react": "^16.8.5",
    "react-dom": "^16.8.5",
    "react-router-dom": "^5.0.0",
    "react-scripts": "2.1.8"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": [
    ">0.2%",
    "not dead",
    "not ie <= 11",
    "not op_mini all"
  ]
}
```
---

### /backend-spring-boot-react-hello-world-with-routing/pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.3.RELEASE</version>
		<relativePath /> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.in28minutes.fullstack.springboot.react.helloworld</groupId>
	<artifactId>spring-boot-fullstack-hello-world-with-routing</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>spring-boot-fullstack-hello-world-with-routing</name>
	<description>Demo project for Spring Boot</description>

	<properties>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>
```
---

### /backend-spring-boot-react-hello-world-with-routing/src/test/java/com/in28minutes/fullstack/springboot/react/helloworld/springbootreacthelloworldwithrouting/SpringBootReactHelloWorldWithRoutingApplicationTests.java

```java
package com.in28minutes.fullstack.springboot.react.helloworld.springbootreacthelloworldwithrouting;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringBootReactHelloWorldWithRoutingApplicationTests {

	@Test
	public void contextLoads() {
	}

}
```
---

### /backend-spring-boot-react-hello-world-with-routing/src/main/resources/application.properties

```properties

```
---

### /backend-spring-boot-react-hello-world-with-routing/src/main/java/com/in28minutes/fullstack/springboot/helloworld/springboothelloworldwithrouting/helloworld/HelloWorldController.java

```java
package com.in28minutes.fullstack.springboot.helloworld.springboothelloworldwithrouting.helloworld;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

//Controller
@RestController
@CrossOrigin(origins = { "http://localhost:3000", "http://localhost:4200" })
//
public class HelloWorldController {

	@GetMapping(path = "/hello-world")
	public String helloWorld() {
		return "Hello World";
	}

	@GetMapping(path = "/hello-world-bean")
	public HelloWorldBean helloWorldBean() {
		return new HelloWorldBean("Hello World From a Java Bean");
	}
	
	///hello-world/path-variable/in28minutes
	@GetMapping(path = "/hello-world/path-variable/{name}")
	public HelloWorldBean helloWorldPathVariable(@PathVariable String name) {
		//throw new RuntimeException("Something went wrong");
		return new HelloWorldBean(String.format("Hello World, %s", name));
	}
}
```
---

### /backend-spring-boot-react-hello-world-with-routing/src/main/java/com/in28minutes/fullstack/springboot/helloworld/springboothelloworldwithrouting/helloworld/HelloWorldBean.java

```java
package com.in28minutes.fullstack.springboot.helloworld.springboothelloworldwithrouting.helloworld;
public class HelloWorldBean {

	private String message;

	public HelloWorldBean(String message) {
		this.message = message;
	}

	public String getMessage() {
		return message;
	}

	public void setMessage(String message) {
		this.message = message;
	}

	@Override
	public String toString() {
		return String.format("HelloWorldBean [message=%s]", message);
	}

}
```
---

### /backend-spring-boot-react-hello-world-with-routing/src/main/java/com/in28minutes/fullstack/springboot/helloworld/springboothelloworldwithrouting/SpringBootFullStackHelloWorldWithRoutingApplication.java

```java
package com.in28minutes.fullstack.springboot.helloworld.springboothelloworldwithrouting;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringBootFullStackHelloWorldWithRoutingApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringBootFullStackHelloWorldWithRoutingApplication.class, args);
	}

}
```
---
