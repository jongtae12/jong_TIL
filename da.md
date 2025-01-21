# DRF
DRF(Django Rest Framework)**에 대한 TIL(Today I Learned)을 작성하고 싶으시군요! DRF는 Django 기반의 강력한 RESTful API 개발 프레임워크로, 웹 개발 시 자주 활용되는 도구입니다. TIL 작성에 도움이 될 수 있도록, 핵심 개념과 실제 작성 시 고려해야 할 사항들을 정리해 드리겠습니다.

## 1. TIL 작성 시 고려해야 할 점
구체적인 학습 내용: 오늘 학습한 내용을 명확하게 기록하세요. 예를 들어, 특정 serializer 클래스를 만들고, view를 작성하여 API를 구현했다면, 어떤 클래스와 메소드를 사용했는지 상세하게 기록합니다.
핵심 개념: DRF의 핵심 개념인 serializer, view, authentication, permission 등을 중심으로 학습 내용을 정리합니다. 각 개념에 대한 이해도를 높이기 위해 예시 코드나 그림을 함께 첨부하면 더욱 효과적입니다.
어려웠던 점: 학습하면서 어려웠던 부분이나 궁금했던 점을 기록하고, 해결 과정을 상세히 설명합니다. 다른 사람들과 공유하고 피드백을 받을 수 있는 좋은 기회가 될 수 있습니다.
실습: 실제 코드를 작성하고 실행하면서 얻은 경험을 기록합니다. 예상치 못한 오류가 발생했을 경우, 어떻게 해결했는지 구체적으로 설명합니다.
참고 자료: 참고한 문서, 블로그, 강의 등을 기록하여 추후 다시 학습하거나 다른 사람들에게 추천할 수 있도록 합니다.
## 2. DRF TIL 예시
오늘 학습 내용: DRF serializer의 nested relationship 구현

오늘은 DRF serializer에서 nested relationship을 구현하는 방법을 학습했다. 예를 들어, User 모델과 Post 모델이 있을 때, User 모델에 ForeignKey로 Post 모델을 연결하여 one-to-many 관계를 설정하고, 이를 serializer에서 표현하는 방법이다.

핵심 개념:

Nested Serializer: 다른 serializer를 내부에 포함하여 복잡한 데이터 구조를 표현하는 방법
Depth Field: nested relationship의 깊이를 조절하여 원하는 만큼의 데이터를 가져오는 방법
코드 예시:
```
Python

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = '__all__'

class UserSerializer(serializers.ModelSerializer):
    posts = PostSerializer(many=True, read_only=True)

    class Meta:
        model = User
        fields = ('id', 'username', 'posts')
```
어려웠던 점:
처음에는 nested relationship의 개념이 어렵게 느껴졌지만, 공식 문서와 예제 코드를 꼼꼼히 살펴보면서 이해할 수 있었다. 특히, Depth Field를 활용하여 원하는 깊이까지 데이터를 가져오는 방법이 인상적이었다.

실습:
위 코드를 바탕으로 실제 API를 구현하고, Postman을 이용하여 결과를 확인했다. 예상대로 User의 정보와 해당 User가 작성한 모든 Post 정보가 JSON 형태로 잘 반환되었다.