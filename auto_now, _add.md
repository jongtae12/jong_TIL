# 🕒auto_now와 auto_now_add

**1. auto_now와 auto_now_add의 사용용**  
**2. auto_now와 auto_now_add 차이점**  

---
## ➤ 사용방법
먼저 사용하는 코드를 보여주겠다.
```
from django.db inmport models

def post(models.Model):
    created_at = models.DateTimeFiled(auto_now_add=True)
    updated_at = models.DateTimeFiled(auto_now=True)
```    
여기서 `auto_now_add`는 모델 인스턴스 생성을 할 때의 시간을 기록하는 것이고  
`auto_now`는 수정, 저장 등을 할 때 시간을 저장하는 것이다.  
  
둘 다 시간을 저장한다는 개념에서 헷갈릴 수 있는데  
실행되는 상황이 다르다는 것을 이해하셔야 한다.
---
## ➤ 차이점
- 생성 시각을 기록해야 할 때  
- 마지막 수정 시각을 기록해야 할 때   
  
  이 두 차이점을 생각하면 두개의 개념이 이해하는데  
  보다 쉬워질 수 있을 것 입니다.
  
**예시**  
우리가 등교시간 출석을 했을 때를 `auto_now_add`  
한 교시가 끝나는 것, 또는 쉬는 시간 이런 것을 `auto_now`  
이런 방식으로 접근하면 이해하기 쉬울 수 있을 것이다