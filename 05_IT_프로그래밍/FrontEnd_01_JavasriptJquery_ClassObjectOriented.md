# FrontEnd_01_JavasriptJquery_ClassObjectOriented

- 참고도서 샘플소스: http://www.webdongne.com/bbs/bbs/board.php?bo_table=wbook_list&wr_id=10  
<br>

## 5. 자바스크립트 클래스와 클래스 단위 프로그래밍

#### 5.1 자바스크립트에서 클래스란
- 자바스크립트에서는 class 키워드 및 class 문법을 지원하지 않음  
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
- 클래스 정의방법 3가지 비교  

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
