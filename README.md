# Diary
Vue study journal

## 2022.08.28

<br>

### 검색어 :

#### 1. 장점 
#### 2. 버전 차이
#### 3. 각 폴더 설명 
#### 4. eslint, prettier 설정법 
#### 5. User Snippets 등록하기
#### 6. 라우트 연결 방식 세 가지 
#### 7. Vue 규칙

<hr>

<br>

#### 1. Vue 장점
 - html, js, css 를 완벽하게 분리해서 관리할 수 있다.  =  유지, 보수, 추가 개발에 대한 복잡도가 단순해짐
 - 양방향 데이터 바인딩이 가능하다. (v-model)

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

<br>

#### 4. eslint, prettier 설정법
.prettierrc 파일 생성 - {"semi": false, "backetSpacing": true, "singleQuote": true"useTabs": false, "trailingComma": "none", "printWidth": 80}
package.json 파일 열기 - "rules": {"space-before-function-paren": "off"}

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
views 에 사용되는 vue 파일은 이름 끝에 View를 붙인다. ex) AboutView.vue
