# Django 마이그레이션 (migrate, makemigrations) TIL 

오늘은 Django의 마이그레이션에 대해 학습했습니다. 마이그레이션은 모델의 변경 사항을 데이터베이스에 반영하는 중요한 기능입니다.

## 핵심 개념

*   **`마이그레이션 (Migration)`:** 모델 변경 이력을 추적하는 파일
*   **`makemigrations`:** 모델 변경 사항을 기반으로 마이그레이션 파일 생성
*   **`migrate`:** 마이그레이션 파일을 데이터베이스에 적용
---
## 사용 방법

### 1. 마이그레이션 생성

모델을 수정한 후 다음 명령어를 실행

```
python manage.py makemigrations
python manage.py makemigrations <앱 이름>
```
**`주의사항`**  
왠만하면 뒤에 앱까지 쓰세요.  
힘들어질 수 있다고 합니다.  

### 2. 마이그레이트 사용

생성된 마이그레이션을 적용  

```
python manage.py migrate
python manage.py migrate <앱 이름>
```
**`주의사항`**  
이건 그냥 무조건 뒤에 앱까지 쓰세요.  
힘들어질 수 있다고 합니다.  

### 3. 특정 마이그레이션까지 사용

말 그대로 어디까지 사용할지 말해주는 것  

```
python manage.py migrate <앱_이름> <마이그레이션_이름>
```

### 4. 마이그레이션 상태 확인
현재 어떤 상태로 되어있는지 확인할 수 있음음
```
python manage.py showmigrations
```
### 5. 전 상태로 되돌리기
전 상태로 되돌아가고 싶을 때 사용

```
python manage.py migrate <앱 이름><번호>
```
### 6. 초기화
그냥 처음으로 되돌리기

```
python manage.py migrate <앱_이름> zero
```
---
**❗결론❗**  
데이터베이스가 매우매우매우 중요하므로 이 부분에 대해서는 꼭 다시 확인하고 가자!  
adasadas
 

