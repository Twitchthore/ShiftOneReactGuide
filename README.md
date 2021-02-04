# ShiftOneReactGuide

*ShiftOne에서 사용하는 React and JSX Design GuideLine 입니다.*


## Table of Contents
1. [Style Guide](#style-guide)
   - [Basic Rules](#basic-rules)
   - [Naming](#naming)
   - [Methods](#methods)
2. [Structure Guide](#structure-guide)
   - [File Structure](#file-structure)
   - [Basic Structure](#basic-structure)     
   - [Templates](#templates)
3. [Css Guide](#css-guide)
4. [State Management](#state-management)
5. [3rd Party Libaries](#3rdparty-libaries)

## Style Guide
### Basic Rules

 - 1파일에는 1개의 React Component를 포함하는 것을 원칙으로 함.
    - 그러나, 연관된 multiple[Staless, or Pure, Components]는 1개의 파일에 허용할수 있음. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
 - JSX 파일 문법을 기본으로 하여 작성하도록 한다.
 - Type Script를 사용하여 작성하도록 한다.(향후 예정임)
 
 ### Naming
 
  - **확장자명** : .jsx 확장자로 작성하도록 한다. eslint: [`react/jsx-filename-extension`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-filename-extension.md).
  - **파일명**: 파스칼케이스(PascalCase)형식으로 작성하도록 한다. E.g., `ShiftOne.jsx`.
  - **레퍼런스명**: 리액트 컴포넌트는 파스칼케이스(PascalCase)로 작성하고, 그 레퍼런스는 카멜케이스(camelCase)로 작성하도록 한다. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)
  
    ```jsx
    // bad
    import shiftOne from './ShiftOne';
    
    //good
    import ShiftOne from './ShiftOne';
    
    //bad
    const ShiftOneItem = <ShiftOne/>;
    
    //good
    const shiftOneItem = <ShiftOne/>;
    
### Methods

  - 화살표 함수를 기본적으로 사용하여 작성합니다. 단, 전달되는 커스텀 컴포넌트가 새로 생성되면서 리랜더링으로 인한 기능저하가 따라오지 않는지 확인하도록 한다.
  ```jsx
    function ItemList(props) {
      return (
        <ul>
          {props.items.map((item, index) => (
            <Item
              key={item.key}
              onClick={(event) => { doSomethingWith(event, item.name, index); }}
            />
          ))}
        </ul>
      );
    }
   ```
## Structure Guide
### File Structure
```
   +--src
         +--containers
         +--views
         +--index.js
         +--App.js
         +--route.js
```     
### Basic Structure
#### App.js
   - Default로 사용할 Layout Component와 Login, Page404 등 각 프로젝트마다 필요하게 될 Page Component를 라우팅 처리해준다.
   ```jsx
   render() {
      return() (
         <BrowserRouter>
            <Switch>
               <Route exact path="/login" name="Login Page" render={props => <Login {...props}/>} />
               <Route exact path="/404" name="Page 404" render={props => <Page404 {...props}/>} />
               <Route path="/" name="Home" render={props => <TheLayout {...props}/>} />
            </Switch>
         </BrowserRouter>
      }
   ```
### route.js
   - 전체 프로젝트에서 사용되는 url과 연관된 컴포넌트의 정보를 담은 파일
   ```jsx
      import Dashboard from './views/dashboard';
      
      const routes = [
         { path: '/', exact: true, name: 'Home' },
         { path: '/dashboard', name: 'Dashboard', component: Dashboard }
       ];
   ```
#### Containes/TheLayout.js
   - 전체 프로젝트에서 사용되는 templates 컴포넌트(AppBar, Navigation, Drawer...)를 유지하면서 Routing에 따라서 View 부분만 inflate해준다. 
   ```jsx
   const TheLayout = () => {
     return (
      <div className="default-layout">
         <TheSidebar/>
         <div className="header-wrapper">
            <TheHeader/>
            <div className="body">
               <TheContent/>
            </div>
            <TheFooter/>
         </div>
      </div>
      )
   }
   ```
#### Containers/TheContent.js
   - url이 변경될시에 routing 처리되어 변경된 view component를 렌더링해준다.
   ```jsx
   const TheContent = () => {
      return(
         <main>
            <Container>
               <Switch>
                  {routes.map((route, idx) => {
                      return route.component && (
                        <Route
                           key={idx}
                           path={route.path}
                           exact={route.exact}
                           name={route.name}
                           render={props => (
                              <route.component {...props} />
                           )} />
                        )
                      })}
                 <Redirect from="/" to="/main" />
               </Switch>
            </Container>
         </main>        
      );
   }
   ```
### Templates
   - 전체 프로젝트에서 공통적으로 사용되는 Layout 컴포넌트들, SideBar, Header, Footer로 구성된다.
#### Containers/TheSidebar.js
   - 왼쪽이나 오른쪽에서 Header에 있는 NavBar와 연동해서 작동하는 Drawer
   ```jsx
   const TheSidebar = () => {
   
   }
   ```
   
