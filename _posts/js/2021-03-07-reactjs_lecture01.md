---
title:  "[React.js] React.js 개념정리 01"
excerpt: "리액트 소개와 툴 정리"  
permalink: /categories/js/reactjs_lecture01
author_profile: true
categories:
  - JS
tags:
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2021-03-07
toc: true
toc_sticky: true
---  

# 💡React.js  
![reactjs-2](/assets/images/reactjs-2.png)     
> 컴포넌트 단위로 이루어진 UI를 만들 수 있는 라이브러리   

# 💡컴포넌트
> 한가지 기능을 수행하는 UI단위  

* 서로 독립적이고 고립되어 있음  
* 재사용이 가능하다 → 유닛테스트 하기 좋다.  
* 트리 형식으로 만들어짐  

## ✔구성
> `state`와 `render()`로 구성된다.  

1. `state`: 데이터를 담고있는 오브젝트  
2. `render()`: 사용자에게 UI를 표기위해 정의하는 함수   

* `state` 상태가 변화할 때마다 `render()` 함수가 계속 반복적으로 호출되어 사용자에게 업데이트된 화면이 제공된다.  
* 가장 상위에 있는 루트 컴포넌트안에 `state`가 변경되면 그 안에 들어있는 자식 요소의 `render`함수도 계속 호출되어 사용자에게 업데이트된 내용이 보여진다.  
  * `Virtul DOM Tree`를 메모리에 보관해 놓고 있기 때문에 이전의 트리와 비교해서 업데이트 되는 내용을 모아서 한번에 다 같이 변경한다.
  → **빠른 성능** 보장(1초 안에 60개의 프레임 업데이트 보장)  
* 데이터가 변경될 때 마다 어플리케이션 전체를 다시 렌더링한다.  

## ✔Virtual DOM Tree란?  
> 리액트 내부의 가상의 Dom Tree  
> 리액트의 컴포넌트들이 가상의 메모리공간에 보관되어져있다.   

![virtualdomtree](/assets/images/virtualdomtree.png)    


```javascript  
import React from 'readct';

class LikeButton extends Component {
    state = {
        numberOfLikes: 0,
    };
    render(){
        return <button>
        {this.state.numberOfLikes}
        </button>;
    }
}
```

# 💡React 공식 사이트
[1. React](https://reactjs.org/docs/getting-started.html)    
[2. Create React App](https://create-react-app.dev/docs/getting-started)   
* 북마크하고 보면서 업데이트된 내용을 항상 체크하자.  


# 💡React Tools  
> 아래 툴들을 모두 설치하자.   

## ✔1. 터미널  
기본적인 터미널 사용 or 윈도우는 cmder 설치    
## ✔2. 깃 설치  
> 소스코드 버전 관리    

```bash  
git --version   
```    
## ✔3. Node.js
> 어느곳에서나 자바스크립트 프로그래밍이 가능하게 하는 프레임워크    

* 백엔드 서버, 서버사이드 렌더링, 커맨드라인 툴 등에 사용  
```bash
node -v
```  
## ✔4. npm
> 외부 라이브러리를 다운로드 받고 업데이트 하게 도와주는 패키지 매니저  

* node.js를 설치하면 같이 설치됨
* `package.json`파일 생성 → 외부라이브러리들과 버전에 대한 정보 담김  
* **[비교]npx**: 설치하는 것이 아니라 우리가 원하는 외부 라이프러리나 패키지를 실행할 수 있게 도와주는 툴.  
```bash
npm -v
```   
## ✔4. yarn  
> npm과 npx대신에 사용할 거임!!  
> 페이스북에서 만들어진 패키지 매니저    

* `npm`에서 부족한 버전관리, 성능, 보안문제 등을 보완함  
* `npm`위에서 동작하므로 `npm`과 호환 가능하며 `pakcage.json` 파일을 그대로 유지
```bash
npm install yarn --global  
yarn -v
```   

## ✔5. creat-react-app
> 페이스북에서 만든, 리액트를 개발하는 수많은 개발자들이 공통적으로 사용하는 정말 유용한 툴들을 한번에 자동적으로 설치할 수 있는 툴   

* [Create React App](https://create-react-app.dev/docs/getting-started/) 대로 진행     

프로젝트를 생성하길 원하는 폴더안에서 터미널 실행     
```bash  
yarn create-react-app "프로젝트 이름"   
```    
![20210307_193232](/assets/images/20210307_193232.png)      


```bash  
yarn start # 실행
yarn build # 실행x 배포
yarn test # 유닛테스트 실행 후 테스트 결과 출력
yarn eject # 내부의 많은 툴 확인,설정 가능  
```    

프로젝트 안에서 `yarn start`를 하게 되면 프로젝트가 실행된다.  

![20210307_193232](/assets/images/20210307_193232.png)   


![20210307_193706](/assets/images/20210307_193706.png)   

서버가 실행되는 동안 새로운 터미널을 열어서 해당 프로젝트 경로안에서 `code .`를 입력해 `VScode`를 실행한다.   


# 💡프로젝트 구조   
![20210307_193937](/assets/images/20210307_193937.png)   
리액트 프로젝트의 구조의 큰 틀은 다음과 같다.   

1. `.gitignore`  
> 깃에 더이상 트래킹하지 않고 싶을 때    

2. `package.json`  
> npm에서 버전을 관리 할 때 외부라이브러리 버전 명시   
3. `dependencies`   
우리가 쓰고 있는 외부 라이브러리    
 
4. `README.md`   
> 프로젝트에 대한 설명    

5. `yarn.lock`  
> yarn을 이용할 경우 자동 생성되는 파일  

6. `node-modules`  
> 외부 라이브러리를 추가했을 대 자동으로 추가됨    

7. `public`  
> 사용자에게 배포할 때 외부적으로 보여지는 대표적인 파일 모음    
 
 * `manifest.json`
  > 프로그래시브 웹 어플리케이션(PWA)을 만들때 필요한 파일  

  * `robots.txt`  
  > 웹 크롤링을 위해 사용되는 파일     

8.  `src`  
> 프로젝트 작업이 주로 진행되는 폴더      

# 💡React의 숨겨진 툴   
위에서 `creat-react-app`으로 리액트를 개발할 때 필요한 바벨, 테스팅에 관련된 것들, 타입 스크립트, eslint, 제스트, postCSS 등이 자동으로 설치되었다.  
이들을 세부적으로 설정하고 싶을 경우 `yarn eject`를 통해 확인할 수 있다.   
주의할 점은 <u>이전 상태로 되돌아갈 수 없으므로</u> 꼭 필요할때만 사용하자.  

## ✔Babel  
![babellogo](/assets/images/babellogo.png)   
> 자바스크립트 트랜스 컴파일러   

* ECMA 이후 버전의 아이들 예전 버전으로 변환해 예전 브라우저가 이해할 수 있도록 해준다.
* JSX를 브라우저가 이해할 수 있도록 javaScript로 변환해준다.  
* 어느정도 버전까지 변환할 것인지 설정 가능  


## ✔Webpack  
![webpackimg](/assets/images/webpackimg.png)  
> 소스코드를 사용자에게 간편하게 전달할 수 있도록 모듈을 번들링함  


## ✔ESLint  
![eslint](/assets/images/eslint.jpg)   
> 코드에 잘못된 부분에 대해 즉각적으로 경고 사인 알림  

## ✔Jest
> 자바스크립트로 코드를 작성할 때 유닛테스트를 할 수 있게 도와주는 테스팅 프레임워크  

## ✔PostCSS  
> CSS 전처리기 중 하나로 자바스크립트로 CSS변환을 해주는 도구    

* less,sass와 비슷하다.  
* sass는 정해진 것들만 할 수 있지만 PostCSS는 다양한 플러그인이 있어 원하는 것 추가 가능   
* 현업에서 많이 쓰임   

# 💡유용한 개발툴  
1. [크롬 확장프로그램 `React Developer Tools`](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=ko,)  
  * 리액트로 만든 사이트에서 활성화됨   
  * 개발툴을 이용해 컴포넌트 구조를 확인할 수 있다.
2. VSCode Extensions
  * reactjs snippet*검색결과 두번째꺼)   
    * rcc단축키 하나로 리액트 컴포넌트 자동 생성  
  * auto import
    * 다른 리액트 컴포넌트 import시 자동 설치  