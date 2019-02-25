# 2019/02/25 업무이슈
- 이슈
  - 제휴사가 이미지 서버를 https로 전환후 여전히 우리쪽 서버가 다운받을 이미지 url를 http로 전달해줌으로 인해 redirect 로 인해 이미지가 제대로 다운되지 않음.
- 해결방법 
(참고링크:https://www.mkyong.com/java/java-httpurlconnection-follow-redirect-example/)
  - 만약 server가 redirect 된다면 응답 코드는 301 또는 302이다. 그리고 redirect 되는 url을 http 응답 header 에 "Location"으로 읽을 수 있다!

~~~
        int status = conn.getResponseCode(); // connection의 response code를 가져옴
    
    	if (status != HttpURLConnection.HTTP_OK) {
    		if (status == HttpURLConnection.HTTP_MOVED_TEMP
    			|| status == HttpURLConnection.HTTP_MOVED_PERM
    				|| status == HttpURLConnection.HTTP_SEE_OTHER)
    		redirect = true;
    	} // redirect 되는 응답 코드인지 판별
    
    	System.out.println("Response Code ... " + status);
    
    	if (redirect) {
    
    		// get redirect url from "location" header field
    		String newUrl = conn.getHeaderField("Location"); // header 에 있는 "Location"을 가져온다!
    
    		// get the cookie if need, for login
    		String cookies = conn.getHeaderField("Set-Cookie");
    
    		// open the new connnection again
    		conn = (HttpURLConnection) new URL(newUrl).openConnection();
    		conn.setRequestProperty("Cookie", cookies);
    		conn.addRequestProperty("Accept-Language", "en-US,en;q=0.8");
    		conn.addRequestProperty("User-Agent", "Mozilla");
    		conn.addRequestProperty("Referer", "google.com");
    								
    		System.out.println("Redirect to URL : " + newUrl);
    
    	}
~~~    	


* HTTP 상태코드 정리
	* 참조링크 
	  * <https://item4.github.io/2018-02-08/Basic-HTTP-Status-Codes/>
	* 더 알아보기 
	  * <https://httpstatuses.com/>
	  * <http://www.restapitutorial.com/httpstatuscodes.html/>
 
| code  |  설명                              |   
|-------|-----------------------------------|                             
| 500   | 서버 내부 에러(Internal Server Error) |  
| 503   | 서비스 지원 불가 (Service Unavailable)  |  
| 400   | 요청 에러 (Bad Request)  |  
| 405   | 잘못된 Method 요청 (Method Not Allowed)  |   
| 404   | 리소스 없음 (404 Not Found)  |  
| 403   | 권한 없음 (Forbidden)  |  
| 429   | 요청이 너무 많음 (Too Many Requests)  |  
| 301   | 접속 주소 이동 (Move Permanently)  |  
| 304   | 바뀐거 없음 (Not Modified)  |  
| 302   | 임시 이전 (Found)  |  
| 200   | 요청 문제 없음 (OK)  | 
| 302   | 요청의 결과 새로운 리소스 생성(바로) (Created)  |    

 
