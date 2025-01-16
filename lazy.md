# 장고 lazy(지연)
## 장고의 Lazy Loading이란?
장고에서 Lazy Loading이란 객체를 실제로 사용하는 순간까지 메모리에 로딩하지 않고, 필요한 시점에 비로소 초기화하는 기법을 의미합니다. 이는 특히 많은 관련 객체를 가진 모델이나 쿼리셋을 다룰 때 메모리 효율성을 높이고 성능을 개선하는 데 효과적입니다.
## get_lazy() 함수
역할: 모델 필드의 값 계산을 지연 평가합니다. 주로 복잡한 계산이나 외부 자원 접근이 필요한 필드에 유용합니다.
사용법: django.utils.functional.get_lazy(func, *result_classes)
func: 지연 평가할 함수.
result_classes: 결과값의 타입 힌트 (예: int, str, float).
```
from django.db import models
from django.utils.functional import get_lazy

def complex_calculation():
    # 매우 복잡한 계산 로직...
    import time; time.sleep(1) # 계산 시간 시뮬레이션
    return 42 * 2

class MyModel(models.Model):
    name = models.CharField(max_length=100)
    calculated_value = models.IntegerField(default=get_lazy(complex_calculation, int))

# 람다 함수를 이용한 간략화
class MyModel2(models.Model):
    name = models.CharField(max_length=100)
    double_name_length = models.IntegerField(default=get_lazy(lambda self: len(self.name) * 2, int))

instance = MyModel(name="Test") # 이 시점에는 계산 X
print(instance.calculated_value) # 이 시점에 complex_calculation() 실행
instance2 = MyModel2(name = "Test")
print(instance2.double_name_length)
```
## lazy() 함수
역할: 더욱 일반적인 상황에서의 지연 평가를 지원합니다. 함수, 메서드, 속성 등에 적용 가능합니다.
사용법: django.utils.functional.lazy(func, *result_classes)
특징: 반환된 객체는 호출 가능한 객체(callable)이므로, 실제 값을 얻기 위해서는 ()를 사용하여 호출해야 합니다.
```
from django.utils.functional import lazy

def expensive_operation():
    print("실행!") # 언제 실행되는지 확인
    return "Result"

lazy_op = lazy(expensive_operation, str)
print("아직 실행 안됨")
result = lazy_op() # 이 시점에 expensive_operation() 실행
print(result) # "Result" 출력
```
## gettext_lazy() 함수
역할: 국제화(i18n)를 위한 문자열 번역을 지연 평가합니다. 템플릿 렌더링 시점에 번역이 수행되므로, 불필요한 번역 부하를 줄입니다.
사용법: from django.utils.translation import gettext_lazy as _ 후 _("번역할 문자열") 형태로 사용
```
from django.utils.translation import gettext_lazy as _
from django.db import models

class MyModel3(models.Model):
    name = models.CharField(max_length=100, verbose_name=_("이름")) # 관리자 페이지 등에 번역된 "이름"으로 표시
```
## 주의 사항 및 요약
과도한 사용은 오히려 오버헤드를 초래할 수 있으므로, 적절히 사용해야 합니다.
지연 평가된 값은 필요에 따라 캐싱하여 중복 계산을 방지하는 것이 좋습니다.
lazy()는 호출 가능한 객체를 반환하므로, 반드시 ()를 붙여 호출해야 합니다.
gettext_lazy()는 국제화된 웹 애플리케이션 개발에 필수적인 요소입니다.