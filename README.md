# Diary
LHW's Vue study journal

## 2022.08.28
- 일기장 전체 틀 작성 및 내용 작성
## 2022.08.29
- 앵귤러, 리액트 단점 추가 및 v-model.number 설명 추가
## 2022.09.23
- 해결했던 에러 두 가지 
<br>

### 검색어 Ctrl + F :

#### 1. 장점 
#### 2. 버전 차이
#### 3. 각 폴더 설명 
#### 4. eslint, prettier 설정법 
#### 5. User Snippets 등록하기
#### 6. 라우트 연결 방식 세 가지 
#### 7. Vue 규칙
#### 8. 다국어 
#### 9. 각종 에러 

<hr>

<br>

사전 주의사항 : vetur 확장팩을 설치
<br>

#### 1. Vue 장점
 - html, js, css 를 완벽하게 분리해서 관리할 수 있다.  =  유지, 보수, 추가 개발에 대한 복잡도가 단순해짐
 - 양방향 데이터 바인딩이 가능하다. (v-model) <br> <strong>앵귤러</strong>: 양방향 데이터 바인딩 지원, 하지만 무거움 <br>  <strong>리액트</strong>: 버츄얼 돔 활용으로 빠름, 하지만 양방향 데이터 바인딩 미지원

<br>

#### 2. vue2 와 vue3 의 버전 차이점
 - 라이브러리가 아직 2에 구현된 종류의 양이 훨씬 많다.
 - template 태그 안에 최상위 div 블럭으로 묶지 않으면 에러가 뜬다. ( 2 )

<br>

#### 3. Vue 각 폴더 설명
 - node_modules : 설치된 node 모듈이 위치해 있는 폴더, npm install 명령어를 통해 설치한 모듈이 위치하는 곳

 - public : index.html 파일이 위치하는 곳 (정적 파일 위치)

 - src : 구현되는 vue 컴포넌트 파일이 위치하는 곳

 - src > assets : css, image 등 파일이 위치하는 곳

 - src > components : Vue 컴포넌트 중 재사용을 위해서 구현된 컴포넌트가 위치하는 곳

 - src > router : 라우팅을 정의하는 파일이 위치하는 곳

 - src > store : vuex의 상태 저장소인 store 파일이 위치하는 곳

 - src > views : 웹 애플리케이션에서 각 화면, 즉 메뉴에 대응되는 화면에 해당하는 Vue 컴포넌트가 위치하는 곳

 - App.vue : 최상위 Vue 컴포넌트

 - package.json : Vue 프로젝트에 대한 정보 및 사용하고 있는 모듈 등에 대한 정보를 관리하고, Vue 프로젝트를 실행할 수 있는 스크립트가 정의된 파일
 	- 이 파일에서 중요한 점은 "node-sass": "^4.12.0" 에서 sass 버전과 호환되는 node.js 를 통해 install 해야 한다는 점이다. 지키지 않을 시 에러.

<br>

#### 4. eslint, prettier 설정법
 - .prettierrc 파일 생성 - {"semi": false, "backetSpacing": true, "singleQuote": true"useTabs": false, "trailingComma": "none", "printWidth": 80}
 - package.json 파일 열기 - "rules": {"space-before-function-paren": "off"}

<br>

#### 5. User Snippets 등록하기
 - File > Preference > User Snippets 메뉴 이동
 - 검색창에 vue 입력
 - 아래 코드 입력

	"Generate Basic Vue Code": {
		"prefix": "vue-start",
		"body": [
			"<template>\n\t<div></div>\n</template>\n<script>\nexport default {\n\tcomponents: {},\n\tdata() {\n\t\treturn {\n\t\t\tsampleData: ''\n\t\t}\n\t},\n\tsetup() {},\n\tcreated() {},\n\tmounted() {},\n\tunmounted() {},\n\tmethods: {}\n}\n</script>"
		],
		"description": "Generate Basic Vue Code"
	}

<br>

#### 6. 라우트 연결 방식 세 가지

###### 1) 무조건 들어가게 되는 페이지의 경우 - 상단에 import 하는 방식 사용
	
	상단 import Homeview from '../views/HomeView.vue'
	
	const routes = [
		{
		path: '/',
		name: 'home',
		component: HomeView
		}
	]

###### 2) 들어갈 가능성이 높거나, 사이즈가 크다. - webpackPrefetch: true
	
	
	const routes = [
		{
		path: '/',
		name: 'home',

		해당 주석은 반복될 필요는 없다. (한 번만 존재하면 됨)
		// route level code-splitting
		// this generates a separate chunk (about.[hash].js) for this route
		// which is lazy-loaded when the route is visited. 
		component: () =>
			import(
 				/* webpackChunkName: "home", webpackPrefetch:true */ '../views/Home.vue'
			)
		}
	]
	

###### 3) 들어갈 빈도가 많지 않거나 자바스크립트 파일 자체가 작다. - webpackPrefetch: true 가 없는 형태
	
	const routes = [
		{
		path: '/',
		name: 'home',
		// route level code-splitting
		// this generates a separate chunk (about.[hash].js) for this route
		// which is lazy-loaded when the route is visited.
		component: () =>
			import(
				/* webpackChunkName: "home" */ '../views/Home.vue'
			)
		}
	]

만약 하나의 webpackChunkName 으로 묶여있다면, 해당 바인딩을 눌렀을 때 그 그룹이 전부 받아짐.
 - 따로 따로 받아서 로딩할 필요가 없이 함께 받아짐
 - 연관성 있는 메뉴들에 효율적으로 적용할 수 있다.
<br>

#### 7. Vue 규칙
 - views 에 사용되는 vue 파일은 이름 끝에 View를 붙인다. ex) AboutView.vue
 - 양방향 데이터 바인딩 : v-model {{텍스트로 인식}}
 - v-model.number {{숫자로 인식}} 
 - v-bind: value 같은 속성에 바인드를 단방향으로 할 때 사용. 이용자가 입력하지 못함. 콜론(:)만 앞에 붙여서 생략하여 사용 가능
 - v-on: 이벤트를 받을 때 사용. @만 앞에 붙여서 생략하여 사용 가능
 
 <br>
 
 #### 8. 다국어 설정
 - 해당 파일의 목표 언어(ko.js) 파일에 export default로 변수 설정 및 해당 값을 설정한 뒤, {{ $t("파일.설정명") }}로 바인딩 작성하여 표시한다.
 <br>
 
 #### 9. 각종 에러 해결
 - npm ERR! code ELIFECYCLE : 1. npm cache clean --force
                              2. rm node_modules
			      3. npm install
			     
 - npm ERR! code ENOENT     : 대부분은 폴더 경로 지정 실수
