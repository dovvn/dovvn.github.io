---
title:  "[React.js] React.js 개념정리 02 - 리액트 기본개념"
excerpt: "리액트 기본 개념"  
permalink: /categories/js/reactjs_lecture02
author_profile: true
categories:
  - JS
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-03-08
toc: true
toc_sticky: true
---  

# 💡클래스 vs 함수 컴포넌트
컴포넌트는 클래스나 함수를 이용해 만들 수 있다.  

## ✔클래스 컴포넌트
> 리액트에서 제공하는 Component라는 클래스를 extends  
> 컴포넌트에 state가 있고 동적인 데이터가 표기될 때 사용   

* `state` 있음  
* `lifecycle methods` 있음: 컴포넌트 상태에 따라서 구현되는 메소드   


```javascript   
class LikeButton extends Component{
    state = {
        numberOf
    }
}
```     

## ✔함수 컴포넌트  
> 간단하게 함수로 만들 수 있다.
> 컴포넌트에 상태가 없고 항상 정적인 데이터가 표기될 때 사용   

* `state`와 `lifecycle methods`모두 없음
    * React 16.8버전에선 React Hook이 등장
      → 함수 컴포넌트 안에서도 `state` 가질 수 있고, `lifecycle methods`도 사용할 수 있음    

```javascript    
function App(){
    return <h1>Hello</h1>
}
```   

## ✔컴포넌트 종류    
* Class   
  * React.Component  
  * React.PureComponent  
  * React Hook   

* Function  
  * function  
  * memo(function) → Higher Order Component(고차 컴포넌트)라고 부른다.    


# 💡템플릿 프로젝트 만들기  
`create react-app`으로 만들어진 프로젝트에서 필요 없는 부분을 지워서 필요한 템플릿 프로젝트를 만들어 보자    

프로젝트의 `public`에는 정적인 파일, `src`에는 동적인 파일이 들어간다.    

* `public`폴더
    * `index.html` 필요없는 부분 정리  
    * `manifest.json` 삭제
    * `robots.txt` 삭제
    * `logo.png`들 삭제
* `src`폴더
    * `serviceWorker.js` 삭제
    * `logo.svg` 삭제
    * `setupTests.js` 삭제  
    * `App.test.js` 삭제  
    * `components` 폴더 생성
    * 모든 폴더 소문자로 변경  
    * `app.js`→`app.jsx`로 변경(순수 자바스크립트와 구분하기 위해서)

 ![20210309_001640](/assets/images/20210309_001640.png)    

<br/><br/>

# 💡프로젝트 만들기
위에서 만든 `template`프로젝트를 복사해서 `habit-tracker`프로젝트를 만들어준다.  
```bash
cp -R template habit-tracker
```

<br/><br/>

# 💡index.js
## react-dom
> React 컴포넌트를 웹 브라우저에 렌더링 하는 API  

* index.html와 index.js를 연결해서 브라우저에 보여지도록 한다.  
* 상위에 컴포넌트를 연결해준다.  
* 컴포넌트 생성은 app.jsx에서 시작하면 됨  


## ✔`<React.StrictMode>`
> 코딩하거나 좀 실수하거나 위험한 상황에 바로 에러메시지가 뜸    

* 배포되었을때는 에러메시지가 뜨지 않음  
* 컴포넌트를 두번 호출해서 잘못된 부분이 없는지 확인한다.  

<br/><br/>

# 💡JSX정리(HTML과의 차이점)  
* JSX는 HTML과 다르게 `className`, `onClick`으로 작성해야 한다.  

```javascript    
function App(){
    return <h1 className="title" onClick="">Hello! :)</h1>
}
```  
* HTML은 마크업 언어, JSX는 자바스크립트 코드이다.
* JSX에서는 비즈니스 로직을 사용할 수 있다. {}사용  
* JSX에서는 두가지의 자식노드를 사용할때 하나로 묶어주어야 한다.
    → `<React.Fragment>`  

    
```javascript  
function App(){
  return(
    //<React.Fragment>와 같음  
    <> 
        <h1>Hello!</h1>
        {name && <h1>Hello! {name} :)</h1>}
        {['♥', '🍎'].map(item => (
            <h1>{item}</h1>
        ))}
    </>
  );
}
```   
<br/><br/>

# 💡Habit컴포넌트 만들기  
* 키보드 `rcc`+`tab`으로 기본적인 컴포넌트 템플릿 구조 생성가능  
* 클래스는 항상 대문자여야함  
* `yarn add @fortawesome/fontawesome-free`로 폰트 설치 
* `ctrl`+`P`로 파일로 빠르게 이동 가능   

<br/><br/>

# 💡State 이해하기  
* `this.setState()`: 데이터를 업데이트 할때 사용
* state가 변경될 때 render() 자동으로 호출  

<br/><br/>

# 💡Props
> 컴포넌트 밖에서 주어지는 데이터  

* 컴포넌트의 재사용성 높임  

```javascript
<LikeButton title={'Like'} onClick={this.handleClick}>
```  

App 부모컴포넌트에서 위와 같이 LikeButton 컴포넌트에 title과 onClick을 인자로 전달해주면 전달된 인자들이 오브젝트로 묶여져서 LikeButton컴포넌트 안에서 `this.props`으로 할당되어진다.  

<br/><br/>

# 💡Habits 컴포넌트 만들기(State up, list key)  
* 자식컴포넌트는 모두 고유한 번호를 가지고 있어야함(배열의 인덱스 사용X)

<br/><br/>

# 💡이벤트 처리하기
* 리액트에서 state를 직접 수정하는것은 좋지 않다.

<br/><br/>

# 💡[Refts and the DOM](https://reactjs.org/docs/refs-and-the-dom.html)
* 리액트에서는 직접 DOM에 접근X, Refts사용
* 멤버 변수 정의 후 원하는 리액트 컴포넌트에 ref로 연결하면 된다.  

<br/><br/>

# 💡[PureComponent](https://reactjs.org/docs/react-api.html#reactpurecomponent)
> 컴포넌트에 state나 props에 변화가 없다면 render함수가 불려지지 않는다.  

* shouldComponentUpdate()를 구현함


