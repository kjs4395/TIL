# spring Interceptor
* 스프링 컨트롤러에서 메서드를 호출하기 전과 후 뷰처리가 끝난 후 등 사이에 실행하는 로직
* Interceptor가 동작하는 과정
	1. Request
	2. DispatcherServlet
		* Servlet Container에서 HTTP프로토콜을 통해 들어오는 모든 요청을 프레젠테이션 계층의 제일앞에둬서 중앙집중식으로 처리해주는 프론트 컨트롤러(front controller)
		* ex) tomcat(servlet container) 가 요청을 받는데 이거를 Dispatcher서블릿이 받아 적절한 세부 컨트롤러로 작업을 위임 
	3. HandlerInterceptor(인터페이스)
		* (3) preHandler()
			* 컨트롤러 실행 직전 동작
			* 반환값이 true이면 정상적 진행 / false이면 실행멈춤 
		* (5) PostHandler()
			* 컨트롤러 진입 후 view가 랜더링 되기 전 수행. 
		* (7) afterCompletion()
			* 컨트롤러 진입 후 view 랜더링 후 제일 마지막에 수행. 
	4. Handler(controller)
	6. View
	8. Response

* spring boot에서 구현을 위해서 

1. HandelrInterceptorAdapter 구현

~~~
public class Test extends HandlerInterceptorAdapter {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
		log.info("Interceptor > preHandle");
		return true;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        log.info("Interceptor > postHandle");
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object object, Exception arg3) throws Exception {
        log.info("Interceptor > afterCompletion" );
    }
}

~~~

2. WebMvcConfigurerAdapter를 상속받은 설정 클래스 구현

~~~

@Configuration
public class WebMvcConfig extends WebMvcConfigurerAdapter {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new Test())
                .addPathPatterns("/*")
                .excludePathPatterns("/test/**/")
                login"); 
    }
}

~~~

