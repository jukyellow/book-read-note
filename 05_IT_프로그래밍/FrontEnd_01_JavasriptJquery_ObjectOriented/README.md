# 효율적 유지보수를 위한 Javascript/Jquery 객체지향 프로그래밍 개발방법

- 참고도서 : Javascript/Jquery 완전정복 3 (정가: 3만2천원)  
- 참고도서 샘플소스: http://www.webdongne.com/bbs/bbs/board.php?bo_table=wbook_list&wr_id=10  
- (20.12.11) 현재 ES6 표준에 class가 존재하지만, IE11에서는 지원하지 않는다. 하여 크롬 및 IE11에서 동작가능한 ES6 이전 문법을 기준으로 본 글을 정리한다.  
- ES6 호환성 : https://kangax.github.io/compat-table/es6/  
<br>

## 5. 자바스크립트 클래스와 클래스 단위 프로그래밍

### 5.1 자바스크립트에서 클래스란
- 자바스크립트에서는 class 문법을 지원하지 않음(ES5 이전), class 기반 언어가 아닌 프로토타입 기반 언어이다.  
- 자바스크립트에서 클래스를 구현하는 방법 3가지 : 리터럴, 함수, 프로토타입   
#### 5.1.1. 리터럴 예제  
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
#### 5.1.2. 함수 예제  
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
#### 5.1.3. 프로토타입 예제  
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
- 참고: 자바스크립트 프로토타입이란?(http://insanehong.kr/post/javascript-prototype/, http://www.nextree.co.kr/p7323/)  
![image](https://user-images.githubusercontent.com/45334819/101923592-f2789a00-3c12-11eb-9797-fc11fb2f24cf.png)  


<br>

#### 5.1.4. 클래스 정의방법(리터럴, 함수, 프로토타입) 별 특징  
**1) 리터럴 방식**  
- 예제: https://github.com/jukyellow/book-read-note/blob/master/05_IT_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/FrontEnd_01_JavasriptJquery_ObjectOriented/5_1_1_literal_exam.html  
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
**2) 함수 방식**  
- 예제: https://github.com/jukyellow/book-read-note/blob/master/05_IT_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/FrontEnd_01_JavasriptJquery_ObjectOriented/5_1_2_funtion_exam.html  
- 개선된 점: 코드 재사용가능  
- 단점: 메소드가 객체마다 중복해서 생성됨  

**3) 프로토타입 방식**  
- 예제 : https://github.com/jukyellow/book-read-note/blob/master/05_IT_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/FrontEnd_01_JavasriptJquery_ObjectOriented/5_1_3_prototype.html    
- 장점 : 코드 재사용 가능, 메소드 공유 가능  
- 기타 : Jquery도 프로토타입 방식 클래스로 구현됨  

#### 5.1.5. 클래스 정의방법 3가지 비교  

|방식|특징|
|:---:|---|
|프로토타입 방식|일반적인 클래스 제작방법|
|              |인스턴스마다 공통된 메서드를 공유해서 사용하는 장점이 있음|
|              |jQuery도 prototype 방식으로 만들어져 있음|
|함수방식|간단한 클래스 제작시 사용|
|       |인스턴스마다 메서드가 독립적으로 만들어지는 단점이 있음|
|리터럴 방식|클래스 만드는 용도는 아니며, 주로 여러 개의 매개변수를 그룹으로 묶어 함수의 매개변수로 보낼 때 사용|
|          |정의와 함께 인스턴스가 만들어지는 장점이 있음. 단 인스턴스는 오직 하나만 만들수 있음|
<br>

### 5.2 클래스 중급
#### 5.2.1 this (메소드를 호출한 객체가 저장되는 속성)
- 상황에 따른 this 객체 저장값  

|this가 만들어지는 경우|this 값|
|---|---|
|1.일반함수에서|window 객체|
|2.중첩함수에서|window 객체|
|3.이벤트에서|이벤트를 발생시킨 객체|
|4.(프로토타입)메소드에서|메소드를 호출한 객체|
|5.(프로토타입)메소드 내부의 중첩 함수에서|window 객체|

``` javascript
<script>
var data=10;
function outer(){
    this.data=20;
    data=30;

    document.write("1. data1 = "+data,"<br>");
    document.write("2. this.data = "+this.data,"<br>");
    document.write("3. window.data = "+window.data,"<br>");
}
outer();
/* 1.출력결과: 1. data = 30, 2. this.data = 30, 3. window.data = 30 */  

$(document).ready(function(){
    // 이벤트 리스너 등록
    $("#myButton").click(function(){
	this.data=20;
	data=30;

	console.log("1. data1 = "+data);
	console.log("2. this.data = "+this.data);
	console.log("3. window.data = "+window.data);
    });
});
/* 3.실행결과  1. data = 30, 2. this.data = 20,  3. window.data = 30 */

// 클래스 정의
function MyClass() {
    // 프로퍼티 정의
    this.data=0;
}
// 메서드 정의
MyClass.prototype.method1=function(){
    this.data=20;
    data=30;
    console.log("1. data1 = "+data);
    console.log("2. this.data = "+this.data);
    console.log("3. window.data = "+window.data);
}
var my1 = new MyClass(); // 인스턴스 생성       
my1.method1();  // 메서드 호출
/* 4.실행결과 : 1. data = 30, 2. this.data = 20, 3. window.data = 30 */
</script>
```

#### 5.2.2 함수호출 vs new 함수호출  
|구분|함수이름()|new 함수이름|
|---|---|---|
|해석|일반함수 호출|new 클래스이름()으로 해석, 특정 클래스의 인스턴스를 생성|
|this내용|window 객체|인스턴스|
  
``` javascript
<script>
var userName ="test";
// 함수 정의
function User(name){
    this.userName=name; // 전역 변수 접근
}
User("ddandongne"); // 호출
console.log("1. uesrName = "+userName); /* 실행결과 :  userName = ddandongne  */
 
var userName ="test";
// 클래스 정의
function User(name){
    this.userName=name; // 프로퍼티 접근.
}
var user = new User("ddandongne"); // 호출
console.log("1. uesrName = "+userName); /* 실행결과 :  userName = test  */
</script>
```

#### 5.2.3 함수단위 코딩 vs 클래스 단위코딩  
- 참고소스: https://github.com/jukyellow/book-read-note/blob/master/05_IT_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/FrontEnd_01_JavasriptJquery_ObjectOriented/5_2_3_class_coding.html  
``` javascript
$(document).ready(function(){
    var tab1 = tabMenu("#tabMenu1");
    tab1.setSelectItemAt(1); // 1번째 탭메뉴 아이템 선택
    var tab2 = tabMenu("#tabMenu2");
    tab2.setSelectItemAt(2);    // 2번재 탭메뉴 아이템 선택
});
function tabMenu(selector){
    var $tabMenu =null;
    var $menuItems=null;
    var $selectMenuItem=null;
    function init(selector){ // 요소 초기화
	$tabMenu = $(selector);
	$menuItems = $tabMenu.find("li");
    }
    function initEvent(){ // 이벤트 등록
	$menuItems.on("click",function(){
	    setSelectItem($(this));
	});
    }
    function setSelectItem($menuItem){ // $menuItem에 해당하는 메뉴 아이템 선택하기
	if($selectMenuItem){ // 기존 선택메뉴 아이템을 비활성화 처리하기
	    $selectMenuItem.removeClass("select");
	}
	$selectMenuItem = $menuItem; // 신규 아이템 활성화 처리하기
	$selectMenuItem.addClass("select");
    }
    function setSelectItemAt(index){ // index에 해당하는 메뉴 아이템 선택하기
    	setSelectItem($menuItems.eq(index)); // setSelectItem() 호출
    }
    init(selector); // 초기화 함수 호출
    initEvent();
    // 기능 리턴
    return  {
	"setSelectItemAt":setSelectItemAt
    }
}

$(document).ready(function(){
            var tab1 = new TabMenu("#tabMenu1"); // 인스턴스 생성
            tab1.setSelectItemAt(1); // 1번째 탭메뉴 아이템 선택
            var tab2 = new TabMenu("#tabMenu2");
            tab2.setSelectItemAt(2); // 2번째 탭메뉴 아이템 선택
        });
        function TabMenu(selector) {
            this.$tabMenu = null;
            this.$menuItems = null;
            this.$selectMenuItem = null;
            this.init(selector); // 요소 초기화 및 이벤트 등록 호출하기
            this.initEvent();
        }
        TabMenu.prototype.init = function(selector) { // 요소 초기화
            this.$tabMenu = $(selector);
            this.$menuItems = this.$tabMenu.find("li");
        }
        TabMenu.prototype.initEvent = function() { // 이벤트 등록
            var objThis = this;
            this.$menuItems.on("click", function() {
                objThis.setSelectItem($(this));
            });
        }
        TabMenu.prototype.setSelectItem = function($menuItem) { // $menuItem에 해당하는 메뉴 아이템 선택하기
            if (this.$selectMenuItem) { // 기존 선택메뉴 아이템을 비활성화 처리하기
                this.$selectMenuItem.removeClass("select");
            }
            this.$selectMenuItem = $menuItem; // 신규 아이템 활성화 처리하기
            this.$selectMenuItem.addClass("select");
        }
        // index에 해당하는 메뉴 아이템 선택하기
        TabMenu.prototype.setSelectItemAt=function(index){
            var $menuItem = this.$menuItems.eq(index);
            this.setSelectItem($menuItem); // 기존 메서드 재사용
        }
```

#### 5.2.4 인스턴스 프로퍼티 메서드 vs 클래스 프로퍼티 메소드  
- 인스턴스 프로퍼티/메소드: new를 통해 객체를 생성한 후 사용하는 방식  
- 클래스 프로퍼티/메소드: java static 변수/함수처럼 인스턴스 생성없이 바로 사용하는 방식(독립적 실행가능한 유틸리티성 기능 구현시 주로 사용)    
``` javascript
function TabMenu(selector) {
    this.$tabMenu = null;
    this.$menuItems = null;
    this.$selectMenuItem = null;
    // 요소 초기화 및 이벤트 등록 호출하기
    this.init(selector);
    this.initEvent();
}
// 탭메뉴 정보 추가
TabMenu.version = "1.0";
TabMenu.getInfo=function(){
    var info = {
	developer:"딴동네",
	email:"ddandongne@webdongne.com",
	desc:"탭메뉴를 구현한 클래스입니다."
    }
    return info;
}
$(document).ready(function(){
    // 인스턴스 생성
    var tab1 = new TabMenu("#tabMenu1");
    tab1.setSelectItemAt(1);
    var tab2 = new TabMenu("#tabMenu2");
    tab2.setSelectItemAt(2);

    console.log(TabMenu.getInfo()); // 정보 출력
});

//다른예1) Math 함수
Math.floor(Math.random()*10); // 0에서 10사이의 랜덤 숫자 만들기
alert(Math.max(10,20)); // 두 수중 큰 숫자 값 알아내기
//다른예2) Jquery trim함수
var data = "   1234  ";     // 문자열 좌우에 공백이 포함되어 있어요.
var result = jQuery.trim(data); // jQuery의 trim() 메서드를 활용해 좌우 공백 제거
alert(result) // 실행결과 = "1234”;
```

#### 5.2.5 패키지  
- java 문법  
``` java
package 패키지명
public class 클래스이름 { ... }
//접근: 패키지명.클래스이름
```
- Javascript 문법 : 패키지 문법 제공하지 않음, 오브젝트 리터럴로 흉내를 내서 사용  
``` javascript
var packageName1 = {} //선언 방법1
var packageName2 = new Object() //선언 방법2
packageName.className = function(){ ... }

//예제
var MyUtil = {}
MyUtil.utils = {}
MyUtil.utils.String = function(){...}
//인스턴스 생성
var myStr = new MyUtil.utils.String();
```

### 5.3 Jquery 플러그인 제작
#### 5.3.1 Jquery 확장  
- 1. 유틸리티: 인스턴스를 생성하지 않고, Jquery 클래스에 직접 접근하여 사용  
``` javascript
//Jquery.유틸리티() or $.유틸리티()
Jquery.trim("  123 AAA "); //123 AAA
```
- 2. 플러그인: Jquery 인스턴스를 생성한 후, 특정 노드를 다루는 기능을 재사용하고자 할때 포장하는 기능  
``` javascript
$("선택자").플러그인(옵션)
var $결과 = $("선택자");
$결과.플러그인(옵션);
```
#### 5.3.2 Jquery 유틸리티 구현  
- 문법(구조)  
``` javascript
(function($){
    $.유틸리티 = function(){...} //기능구현
})(jQuery)
```
- 예제  
``` javascript
(function($){
$.addComma=function(value){
    var data = value+""; // 숫자를 문자로 형변환;
    var aryResult = data.split(""); // 문자를 배열로 만들기
    var startIndex = aryResult.length-3; // 배열 요소를 뒤에서 3자리 마다 콤마 추가하기
    for(var i=startIndex;i>0;i-=3) {
	aryResult.splice(i, 0, ",");
    }
    return aryResult.join(""); // 결과 값 리턴
}	
})(jQuery);
$(document).ready(function(){
document.write("1234 =>", $.addComma("1234"), "<br>");   //1234 =>1,234
document.write("12345 =>", $.addComma("12345"), "<br>"); //12345 =>12,345
});
```
#### 5.3.3 Jquery 플러그인 구현  
- 문법(구조)  
``` javascript
(function($){
    $.fn.플러그인이름 = function(속성값){ // $.fn은 prototype의 닉네임으로 선언됨(Jquery.fn = Jquery.prototype = function(){ ... })
        this.each(function(index){ // Jquery 인스턴스(노드)에서 호출함으로, this는 Jquery 객체 자체 -> Jquery에서 선언된 each(반복탐색)를 호출
	    //기능구현
	}
	return this; // Jquery 체인을 위해 다시 반환, ex: $.플러그인이름.또다른기능()
    }
})(Jquery)
```
- 예제 : https://github.com/jukyellow/book-read-note/blob/master/05_IT_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D/FrontEnd_01_JavasriptJquery_ObjectOriented/5_3_3_plugin_removeAni.html  
``` javascript
// 플러그인 만들기
(function($){
    $.fn.removeAni=function(){
	this.each(function(index){ // 요소 개수만큼 루프 실행
	    var $target= $(this); // 현재 요소 얻기
	    $target.delay(index*1000).animate({ // 딜레이(index*1000) 후 애니메이션 실행
		height:0
	    },500,function(){
		$target.remove(); // 애니 종료 후 현재 요소 제거
	    })
	})
	return this;
    }
})(jQuery)
$(document).ready(function(){
    $(".menu li").removeAni(); // removeAni() 플러그인 호출
});
```
#### 5.3.4 Jquery 클래스 기반 플러그인  
#### 5.3.5 Jquery 플러그인 그룹   
#### 5.3.6 Jquery extend()를 활용한 플러그인 옵션처리
- 예제  
``` javascript
```

<br>
<br>

## 6. 자바스크립트 객체지향 프로그래밍   

### 6.1 객체지향 프로그래맹 특징 4가지(추상화, 캡슐화, 상속, 다형성)  

### 6.2 자바스크립트 캡슐화(javascript 언더바 컨벤션, 클로저(추가))  

### 6.3 자바스크립트 상속

### 6.4 자바스크립트 다형성  

### 6.5 합성  

<br>
