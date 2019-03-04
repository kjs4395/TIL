# JQuery - AJAX 정리
~~~
$.ajax({
  type	: "GET", //요청 메소드 타입
  url		: "url", //요청 경로
  async : true, //비동기 여부
  data  : {key : value}, //요청 시 포함되어질 데이터
  processData : true, //데이터를 컨텐트 타입에 맞게 변환 여부
  cache : true, //캐시 여부
  contentType : "application/json", //요청 컨텐트 타입 "application/x-www-form-urlencoded; charset=UTF-8"
  dataType	: "json", //응답 데이터 형식 명시하지 않을 경우 자동으로 추측
  beforeSend  : function(){
    // XHR Header를 포함해서 HTTP Request를 하기전에 호출됩니다.
  },
  success	: function(data, status, xhr){
    // 정상적으로 응답 받았을 경우에는 success 콜백이 호출되게 됩니다.
    // 이 콜백 함수의 파라미터에서는 응답 바디, 응답 코드 그리고 XHR 헤더를 확인할 수 있습니다.
  },
  error	: function(xhr, status, error){
  	// 응답을 받지 못하였다거나 정상적인 응답이지만 데이터 형식을 확인할 수 없기 때문에 error 콜백이 호출될 수 있습니다.
  	// 예를 들어, dataType을 지정해서 응답 받을 데이터 형식을 지정하였지만, 서버에서는 다른 데이터형식으로 응답하면  error 콜백이 호출되게 됩니다.
  },
  complete : function(xhr, status){
    // success와 error 콜백이 호출된 후에 반드시 호출됩니다.
    // try - catch - finally의 finally 구문과 동일합니다.
  }
});
~~~

# Spring Controller
* 다양한 데이터 형식으로 응답하기 위해 메세지 컨버터라는 것을 지원한다.
* 스프링 3 이상부터 jackson 라이브러리를 의존성으로 추가할 경우 자동적으로 MappingJacksonHttpMessageConverter를 적용해준다.

* @RequestMapping
 * 요청/응답과 관련된 프로퍼티 설정
 * method 
 		* 어떠한 요청 타임을 처리할 것인가를 결정(GET, POST, PUT, DELETE)
 		* ex) RequestMethod.GET

 * produces 
 		* 어떠한 데이터 형식으로 응답할것인가를 결정
 		* ex) produces=MethodType.APPLICATION_JSON_VALUE

 * consumes
 		*  어떠한 요청에 대해서 처리할 것인가
 		*  ex) consumes=MediaType.APPLICATION_JSON_VALUE

 		
* @ModelAttribute, @RequestMapping
	* GET 과 DELETE 요청에서 활용. 파라미터 값을 확인해서 데이터 바인딩.
* @RequestBody
	* POST와 PUT 처럼 데이터가 HTTP요청 바디에 포함되는 경우에 데이터 바인딩
* @RestController
	* 스프링 4부터 지원. 해당 컨트롤러의 메소드들에 @ResponseBody 어노테이션을 적용. 
	 		 	

# Content-type
* application/json
	* {key: value} 형태로 전송
* application/x-www-form-urlencoded
   * key=value&key=value 형태로 전송
   * body를 encoding하는 거는 필수이다.(대부분의 브라우저에서 기본적으로 encoding 하도록 구현 되어있지만 application logic 에서 자동으로 되는지 확인 후 해줘야한다.