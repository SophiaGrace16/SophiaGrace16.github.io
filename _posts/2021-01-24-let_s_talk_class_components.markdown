---
layout: post
title:      "Let’s Talk Class Components"
date:       2021-01-24 23:22:23 +0000
permalink:  let_s_talk_class_components
---

## The Fundamentals of React

Some of the most fundamental building blocks of React are components. Components let you split the user interface into isolated and reusable chunks. For me, my understanding of components began to solidify when I started to visualize it:

![](https://i.imgur.com/Bqs8bGZ.png)

I have “highlighted” each different Component of the page to help you visually see the individual components. It comes together much like a puzzle would. By isolating our code into various parts, we can create cleaner and better-organized code. As I began to develop my portfolio project, I found that I tended to write class components over anything. Class components have state, life-cycle methods and can contain custom class methods. Now on principle, you don’t always need those three things, so sometimes it is better to use a different type of Component. To avoid life-cycle checks, you would use a functional component - which I also used a few places. However, as I am still new to React-Redux, I prefer to keep things more straightforward. Below are four examples of class components; each number correlates to the photo above:

**1. Navigational Bar:**

```
import React, { Component } from 'react'
import { NavLink } from 'react-router-dom';

class NavBar extends Component {
  render() {
    return (

      <nav>

        <div>
          <img src="https://i.imgur.com/rNcgEZG.png" className="signature" />
        </div>
        
        <div className="nav-links">
            <NavLink to="/" className="navbutton">Home</NavLink>
            <NavLink to="/resume" className="navbutton">Resume</NavLink>
            <NavLink to="/projects" className="navbutton">Portfolio</NavLink>
        </div>
            
      </nav>

    )
  }
}

export default NavBar
```

**2. Introduction**:

```
import React, { Component } from 'react'
import PictureWall from '../components/PictureWall'

class Intro extends Component {
  render() {
    return (
      <div className="intro">

        <div className="intro-wrapper">

          <div className="hello-spot">
            <img src="https://i.imgur.com/sx2LiIl.png" className="hello-img"/>
          </div>

          <div className="about-me">

            <b className="about-title">About Me</b>

            <p>
              <b className="about-subtitle">Teacher turned Fullstack Developer</b>
            </p> 

            <p>
              I am experienced in Ruby on Rails and JavaScript based programming. I have a passion for creating innovative, attractive, and functional websites- starting from the initial idea to the design and concept, and finally, creating a finished product. 
              I am a determined and dedicated life-long learner adept in a wide array of programming languages & web tools.
            </p>
             
          </div>
        
        </div>

        <div className="picture-wall">
            <PictureWall/>
        </div>

      </div>

    )
  }
}

export default Intro
```

**3. Picture Wall:**

```
import React, { Component } from 'react'

class PictureWall extends Component {
  render() {
    return (
    <div className="picture-wrapper">
        <div className="pw">
            <img src="https://i.imgur.com/uot3WlQ.png" className="pw-img-first"/>
        </div>

        <div className="pw">
            <img src="https://i.imgur.com/EO7kZtH.png" className="pw-img"/>
        </div>

        <div className="pw">
            <img src="https://i.imgur.com/ptothF3.png" className="pw-img"/>
        </div>

        <div className="pw">
            <img src="https://i.imgur.com/AuraHD6.png" className="pw-img"/>
        </div>

        <div className="pw">
            <img src="https://i.imgur.com/MiOByUd.png" className="pw-img"/>
        </div>

        <div className="pw">
            <img src="https://i.imgur.com/U0RCHeY.png" className="pw-img-last"/>
        </div>

    </div>
    
    )
  }
}

export default PictureWall;
```

**4. Footer:**

```

class Footer extends Component {
  render() {
    return (
      <footer className="footer">
          <a href='http://sophia-white.com' target="_blank"><img src="https://i.imgur.com/bFicN8G.png" className="social"></img></a>
          <a href='https://github.com/SophiaGrace16' target="_blank"><img src="https://i.imgur.com/WkNFQDy.png" className="social"></img></a>
          <a href='http://sophiagrace16.github.io/' target="_blank"><img src="https://i.imgur.com/n8cA9Bg.png" className="social"></img></a>
          <a href='http://linkedin.com/in/sophia-g-white/' target="_blank"><img src="https://i.imgur.com/mV4NKRL.png" className="social"></img></a>
          <a href='https://www.youtube.com/channel/UCGRRLKfNp8u-MVgklh-mgFw' target="_blank"><img src="https://i.imgur.com/IZFgBQ7.png" className="social"></img></a>
          <a href='mailto:sophia.g.white@outlook.com' target="_blank"><img src="https://i.imgur.com/26thL2W.png" className="social"></img></a>
      </footer>
    )
  }
}

export default Footer
```

Even though it is a class component in every instance, we can use it differently depending on the situation. Every class component has the same base formula:


```
class jediTemple extends Component (you can also say - React.Component - here) {
 render() {                      **This is where we say hey Component, this is what you will render**
 return <h1> Hello There!</h1>;    **The return is where you put what you want to be posted to the page **
 }
}
```


You can also call other class components in the return like below:

```
   <div className="picture-wall"> (You don’t need the className but it is good for CSS!)
            <PictureWall/>
        </div>
```

Class components are fantastic Components to start with. They are predictable and have all the different functions you would possibly need. You can always rewrite code and adjust function type as you develop. However, you could create a whole application using only class components. Now whether or not that is the best idea is up to you to decide. 
