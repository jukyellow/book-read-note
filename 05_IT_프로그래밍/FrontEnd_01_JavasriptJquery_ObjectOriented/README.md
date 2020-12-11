# 효율적 유지보수를 위한 자바스크립트 객체지향 프로그래밍 개발방법

- 참고도서 샘플소스: http://www.webdongne.com/bbs/bbs/board.php?bo_table=wbook_list&wr_id=10  
- (20.12.11) 현재 ES6 표준에 class가 존재하지만, IE11에서는 지원하지 않는다. 하여 크롬 및 IE11에서 동작가능한 ES6 이전 문법을 기준으로 본 글을 정리한다.    
<br>

## 5. 자바스크립트 클래스와 클래스 단위 프로그래밍

#### 5.1 자바스크립트에서 클래스란
- 자바스크립트에서는 class 문법을 지원하지 않음(ES6 이전), class 기반 언어가 아닌 function 기반 언어이다.    
- 자바스크립트에서 클래스를 구현하는 방법 3가지 : 리터럴, 함수, 프로토타입   
1. 리터럴 예제  
``` javascript
var user = {
	name:"ddandonge",
	age: 10,
	showInfo:function(){
		document.write("name = "+this.name+", age = "+this.age);
	}
}    
user.showInfo();  // 메서드 호출
```
2. 함수 예제  
``` javascript
// 클래스 정의
function User(){
	this.name="ddandonge";
	this.age = 10;
	this.showInfo=function(){
		document.write("name = "+this.name+", age = "+this.age);
	}
}		
var user = new User(); // 인스턴스 생성		
user.showInfo(); // 메서드 호출
```
3. 프로토타입 예제  
``` javascript
// 클래스 생성자
function User(){
	// 프로퍼티 정의
	this.name="ddandonge";
	this.age = 10;
}
// 메서드 정의
User.prototype.showInfo = function(){
	document.write("name = "+this.name+", age = "+this.age);
}		
var user = new User(); // 인스턴스 생성		
user.showInfo(); // 메서드 호출 
```

- 클래스 정의방법(리터럴, 함수, 프로토타입) 별 특징  
##### 5.1.1 리터럴 방식
- 예제: https://github.com/jukyellow/book-read-note/blob/master/05_IT_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/FrontEnd_01_JavasriptJquery_ObjectOriented/02_06_%EC%98%88%EC%A0%9C02_%EB%8B%A8%EC%9D%BC%ED%83%AD%EB%A9%94%EB%89%B4_%EB%8B%A8%EA%B3%8406_%EA%B0%9D%EC%B2%B4%EC%99%B8%EB%B6%80%EC%97%90%EC%84%9C_%ED%94%84%EB%A1%9C%ED%8D%BC%ED%8B%B0%EC%99%80%EB%A9%94%EC%84%9C%EB%93%9C_%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0.html  
- 단점: 중복코드가 많아짐  
- 활용: 매개변수를 하나로 묶을때 유용 
``` javascript
var userInfo = {
	userName:"김춘경",
	id:"ddandongne",
	age: 20,
	address:"서울시 금천구",
	nickName:"딴동네"
}
showInfo(userInfo); // 함수 호출
function showInfo(userInfo){ // 함수에서 데이터 사용
	document.write("name = "+userInfo.userName, "id = "+userInfo.id, ", nickName = "+userInfo.nickName, ", age = "+userInfo.age, ", address = "+userInfo.address);
}
```

- 클래스 정의방법 3가지 비교  
|방식|특징|
|:---:|---|
|프로토타입 방식|일반적인 클래스 제작방법|
|              |인스턴스마다 공통된 메서드를 공유해서 사용하는 장점이 있음|
|              |jQuery도 prototype 방식으로 만들어져 있음|
|함수방식|간단한 클래스 제작시 사용|
|       |인스턴스마다 메서드가 독립적으로 만들어지는 단점이 있음|
|리터럴 방식|클래스 만드는 용도는 아니며, 주로 여러 개의 매개변수를 그룹으로 묶어 함수의 매개변수로 보낼 때 사용|
|          |정의와 함께 인스턴스가 만들어지는 장점이 있음. 단 인스턴스는 오직 하나만 만들수 있음|




#### 5.2 클래스 중급
- this  
- 함수호출 vs new 함수호출  
- 함수단위 코딩 vs 클래스 단위코딩  
- 인스턴스 프로퍼티 메서드 vs 클래스 프로퍼티 메소드  
- 패키지  

#### 5.3 Jquery 플러그인 제작
- Jquery 확장   
- Jquery 유틸리티 구현  
- Jquery 플러그인 구현  

<br>
<br>

## 6. 자바스크립트 객체지향 프로그래밍   

#### 6.1 객체지향 프로그래맹 특징 4가지(추상화, 캡슐화, 상속, 다형성)  

#### 6.2 자바스크립트 상속

#### 6.3 자바스크립트 다형성  

#### 6.4 합성  

<br>
