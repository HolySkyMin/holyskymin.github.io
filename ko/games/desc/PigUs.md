# 돼지, 우리

<img src="/assets/images/PigUs_banner.png" width=100%>

<div style="display:flex; flex-flow:row wrap;">
    <md-block style="min-width:fit-content; max-width:570px; flex:1">
        ## 게임 정보
        - **장르**: 어드벤쳐, 스토리텔링
        - **플랫폼**: PC, 모바일
        - **게임 엔진**: Unity 2018.4
        - **개발 기간**: 2019. 3. ~ 2019. 7. (4개월)
        - [GitHub에서 보기](https://github.com/HolySkyMin/PigUs)
          - 스토어 배포를 위해 Unity 2022.3 버전으로 판올림되었다.
    </md-block>
    <md-block style="width:250px;">
        ## 다운로드
        <div style="width=100%; max-width:250px;">
            <a href="https://play.google.com/store/apps/details?id=org.teamporkbelly.pigus" target="_blank" style="text-decoration:none;">
                <img src="/assets/images/icons/dlbadge_google_ko.png" width=100%/>
            </a>
            <a href="https://apps.apple.com/kr/app/%EB%8F%BC%EC%A7%80-%EC%9A%B0%EB%A6%AC/id1474252822" target="_blank" style="text-decoration:none;">
                <img src="/assets/images/icons/dlbadge_apple_ko.svg" width=100%/>
            </a>
        </div>
    </md-block>
</div>

## 개요
"돼지, 우리"는 우리에 갇힌 돼지들의 이야기를 다루는 스토리텔링 어드벤쳐 게임이다. 당신 역시 한 마리 돼지로, 매번 선택의 순간을 마주하게 된다.
더 많은 음식과 주인의 사랑을 갈구하면서 살아갈 것인가, 아니면 이 빌어먹을 세상에 반기를 들 것인가?
다른 돼지들을 만나고 그들의 이야기를 들어보자. 선택은 당신의 몫이다.

## 제작 정보
본 작품은 2019학년도 1학기 서울대학교 정보문화학 "게임의 이해"의 학기 프로젝트로 제작되었다.
5명이 팀을 이뤄 본 작품을 제작했으며, 본인은 이 작품의 프로그래밍을 맡았다.

PC 플랫폼으로 제작하여, 2019년 1학기 정보문화학 과제전 ["그 많던 과제는 누가 다 했을까?"](https://www.facebook.com/itctfestival/posts/pfbid0x3smwR6WpFWfArjg2uN7P97VvBDpmxp1AfUC6VwBN152hhBL1LVuhKRtTKFaBBEJl)에 출품하였다. 이후 추가적인 작업과 모바일 플랫폼 포팅을 거쳐 플레이 스토어, 앱 스토어에 무료 게임으로 출시하였다.

## 개발 회고

### 비동기 프로그래밍의 명암
2018년까지 여러 게임들을 프로그래밍하면서 겪은 경험을 토대로, 2019년의 나는 "트렌디한" 코딩을 하는 것에 빠져 있었다.
이 때 내가 적극적으로 사용한 것이 C#의 `async`와 `await` 키워드였다.
이 키워드가 붙은 메서드를 실행할 때에는 실행이 완료될 때까지 '기다릴' 수 있는데, 이를테면 메시지 박스를 보여주는 아래 코드와 같이 활용할 수 있다.
```cs
// 메시지 박스를 보여주고, 유저가 선택할 때까지 기다립니다.
// response는 유저가 선택한 값입니다.
var response = await MessageBox.Show(...);
```
똑같은 기능을 Unity의 코루틴(`Coroutine`)을 사용해 구현하고자 하면 아래와 같은데,
```cs
// 메시지 박스 클래스에서
IEnumerator Show(..., Action<string> callback)
{
    // 보여주고 기다리는 과정 생략
    callback(response);
}
// 메시지 박스를 호출하는 오브젝트에서
// msgbox는 MessageBox 인스턴스입니다.
StartCoroutine(msgbox.Show(response =>
{
    // 유저의 입력을 여기서 처리합니다.
}));
```
코드의 직관성이 확 올라간 것이 느껴질 것이다.
이런 것 때문에 당시의 나는 코루틴 사용을 가능한 한 피하고, 대신 비동기 키워드를 활용하는 것이 이상적이라고 생각했다.

그런 가운데 "돼지, 우리"가 개발되었다. "돼지, 우리"의 플레이 루틴은 일종의 대화와 같이 구현된 상황 스크립트가 재생되고,
유저가 2개의 선택지 중 하나를 택하여 그에 따라 각종 파라미터를 조정하는 것의 반복이다.
따라서 게임 전반적으로 유저의 선택을 기다리는 상황이 자주 나오는데, "돼지, 우리"에서는
이러한 경우를 `async`와 `await`를 사용하여 구현하였다. 다만 비동기 키워드에는 전염성이 있는데,
비동기 메서드를 기다리기 위해서는 해당 메서드를 호출하는 메서드 역시 비동기 메서드여야 한다는 것이다.
이 때문에, 결과적으로는 코드가 아래와 같아진다.
```cs
// IngameManager.cs

private void Start()
{
    UpdateRoutine();
}

public async void UpdateRoutine()
{
    // 게임 로직이 이 안에 들어갑니다.
}
```
게임의 모든 로직이 비동기 메서드 안에 들어가 있고, 이 메서드는 그 안에서 다른 여러 가지 비동기 메서드들을 기다려 가며 동작한다.
대표적으로, 이 메서드(`UpdateRoutine`)가 가장 일반적으로 하는 일은 상황 스크립트의 동작이 완료되는 것을 기다리는 것이다.
자, 이렇게 코루틴을 쓰지 않는 아주 "트렌디한" C# 코드가 완성되었다!

...그런 것처럼 보였다. 하지만 개발을 진행해 나가면서, 분명히 한 번만 넘어가야 할 대화가 두 번씩 넘어가거나,
원래와는 다른 대화 스크립트가 출력되는 등 예기치 못한 문제가 계속 발생하였다.
결론부터 말하자면, 이렇게 게임 로직을 작성하면 안 되는 거였다. 그렇다면 어째서일까?

근본적으로, C#의 비동기 작업과 Unity의 오브젝트 라이프사이클은 연결되어 있지 않다.
Unity에서 오브젝트를 없앨 때, 오브젝트에 달려 있는 각종 컴포넌트와 해당 오브젝트에서 돌아가는
모든 코루틴 작업이 같이 없어진다. 이것들은 Unity의 라이프사이클과 연결되어 있기 때문이다.

하지만 `async`와 `await`를 사용하여 만든 비동기 메서드는 오브젝트를 삭제해도 사라지지 않는다.
한 번 호출된 비동기 메서드는 해당 메서드의 작업이 끝나지 않는 한 계속해서 메모리에 상주해 돌아가게 된다.
만약 추후 해당 메서드를 담고 있는 오브젝트가 다시 생성되면, 메모리에 버티고 있던 비동기 메서드가
다시 살아나, 게임의 각종 액션에 반응하게 된다. 이 때문에 작업이 두 번 발생하거나 하는 문제가 생긴다.
더욱이, 이렇게 홀로 남겨진 메서드는 누구도 건드릴 수 없기 때문에, 메모리 누수의 위험까지 있다.

이를 해결하려면 실행된 비동기 메서드가 어떻게든 `return`을 통해 종료되도록 해야 한다.
"돼지, 우리"에 적용된 해결책은 인게임에 임의의 번호를 붙이고, 비동기 로직의 매 단계마다
인게임 번호를 비교해 번호가 다르면 즉시 종료하도록 하는 것이었다.
```cs
// IngameManager.cs

private void Awake()
{
    // 전략
    int gnum;
    do { gnum = Random.Range(100000000, 1000000000); }
    while (gnum == LastGameNum);
    MasterGameNum = gnum;
    LastGameNum = MasterGameNum;
    Debug.Log("Entered ingame #" + MasterGameNum);
    // 후략
}

public async void UpdateRoutine()
{
    int mynum = MasterGameNum;
    // 매 단계마다
    if (mynum != MasterGameNum)
    {
        Debug.Log("Succesfully escaped async root method of ingame #" + mynum);
        return;
    }
}
```
하지만 애초부터 코루틴 등을 이용해 작성했다면, 앞서 설명한 문제를 피하고 코드 자체도 더 간결하게 쓸 수 있었을 것이다.
이러한 과정을 한 번 거치고 난 뒤, 이후 프로젝트에서는 모든 상황에서 비동기 키워드를 적용하는 것을 피하고,
꼭 필요한 때에만 사용하는 방식으로 작업을 진행하였다.