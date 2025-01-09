# 📃 Django URL
## URL이란?

- **URL은 인터넷 상의 자원(웹페이지,이미지 등)의 위치를 나타내는 주소**  
- **요청한 URL을 통해서 적절한 뷰를 찾아 보여줌**
### 작동 방식
1.  urlpatterns에서 path를 통해 요청된 url을 찾는다.
2. 연결된 앱이나 views를 찾아 넘긴다.
3.  요청 값을 render,response 하여 보여준다.
4. render를 할 시 템플릿의 html을 받아서 보여준다.

### 구성요소
- urlpatterns  
url과 매칭시키는 곳
- views  
urlpatterns에서 넘겨받아 요청을 응답 처리
- templates  
views에게 html문법을 넘겨줌

### 앱 분리
- **앱을 분리하여 각각의 URL을 수행할 수 있도록 구성 및 정리하는 것**  

    앱이 분리가 되면서 URL도 목적에 맞게 분리시키는데  
    이 때 `include`를 통해서 각 앱의 urls.py에 연결
      
    **⭐ 분리된 앱도 프로젝트의 urls.py와 동일하게 urlpatterns를 생성해야함 ⭐**  
      
    **`include`를 통해서 요청을 할 때**  
      
    먼저 요청이 온 url을 프로젝트의 urlpatterns가 살펴서 해당 url이 포함된 include에 넘겨  
    해당 앱의 urls.py로 이동 거기서 추가적인 url을 살펴서 view를 찾음.  
    
    이 때 주의해야 할 점이 있는데  
    include는 이미 앞에 url을 참고했기에 앱의 url에서는 이미 처리가 된 상태로 넘어옴  
       
    **무슨말이야 이게?**  
    예를 들어 user/my_web/ 라는 곳을 프로젝트에서 include를 통해 user를 찾고  
    앱에서는 my_web/을 확인하는 것이다.  
    그렇기 때문에 앱에서 include에서 찾은 url을 중복해서 사용하는 일은 없도록 하자! 

