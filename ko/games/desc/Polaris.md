# Polaris - The Story of Stars -

<img src="/assets/images/Polaris_banner.png" width=100%>

<div style="display:flex; flex-flow:row wrap;">
    <md-block style="min-width:fit-content; max-width:570px; flex:1">
        ## 게임 정보
        - **장르**: 캐릭터 수집
        - **플랫폼**: 모바일
        - **게임 엔진**: Unity 2017.4
        - **개발 기간**: 2018. 8. ~ 2020. 12. (2.5년)
        - [GitHub에서 보기](https://github.com/HolySkyMin/Polaris)
          - 스토어 배포를 위해 Unity 2022.3 버전으로 판올림되었다.
    </md-block>
    <md-block style="width:250px;">
        ## 다운로드
        <div style="width=100%; max-width:250px;">
            <a href="https://play.google.com/store/apps/details?id=com.snugdc.polaris" target="_blank" style="text-decoration:none;">
                <img src="/assets/images/icons/dlbadge_google_ko.png" width=100%/>
            </a>
            <a href="https://apps.apple.com/app/polaris-the-story-of-stars/id6670620923" target="_blank" style="text-decoration:none;">
                <img src="/assets/images/icons/dlbadge_apple_ko.svg" width=100%/>
            </a>
        </div>
    </md-block>
</div>

## 개요
"Polaris - The Story of Stars"는 모바일 플레이에 적합한 캐릭터 수집형 게임이다.
총 33명의 캐릭터와 각 캐릭터마다의 스토리를 모으는 것이 게임의 목표이다.
이 게임의 특징적인 요소는 '관측' 기능으로, 시간을 들여 밤하늘을 관측하는 것으로 관측한 영역에 따라 캐릭터를 획득할 수 있다.

## 제작 정보
"Polaris - The Story of Stars -"는 서울대학교 게임개발동아리(SNUGDC) 내부 활동으로 제작되었다.
개발 당시 SNUGDC의 대형 프로젝트로, 많은 동아리원들이 특히 기획, 아트 쪽으로 이 프로젝트에 기여하였다.
따라서 정확한 제작 인원의 추산은 현재로서는 거의 불가능하며, 작업 기록을 통해 확인한 제작 인원은 아래와 같다.

<details>
    <summary><b>제작 인원 목록 상세보기</b></summary>
    <md-block>
        - **기획**  
          - **시스템 기획**: 김민정
          - **캐릭터 스토리**: 구자현, 김민정, 명소정, 문보성, 윤난새, 홍성민
        - **아트**
          - **캐릭터**: 강다현, 김민정, 김민지, 김지담, 류승희, 명소정, 이강현
          - **그 외**: 김민정, 이강현
        - **프로그래밍**
          - **메인(시스템 등)**: 홍성민
          - **보조**: 손명진, 정상현
        - **PM**: 윤난새
    </md-block>
    <md-block>
        프로젝트를 긴 시간 이끈 주요 제작 인원을 추리면 다음과 같다.
        - **주요 개발진**: 김민정, 명소정, 손명진, 윤난새, 이강현, 홍성민
    </md-block>
</details>

본인은 이 프로젝트의 메인 프로그래머였으며, 일부 기능의 구현에 있어 아이디어적 도움을 받았지만
실제 인게임 코드의 대부분을 본인이 작성하였다.

2019년 진행된 [스마일게이트 멤버십(SGM)](https://careers.smilegate.com/student/membership) 창작 부문 11기 과정에 본 작품으로 참여하였다.

## 스크린샷

<div style="display:flex; flex-flow:row wrap; justify-content:center;">
    <img src="/assets/images/ss/Polaris_1.png" width=49%; style="max-width:238px; margin:1px"/>
    <img src="/assets/images/ss/Polaris_2.png" width=49%; style="max-width:238px; margin:1px"/>
    <img src="/assets/images/ss/Polaris_3.png" width=49%; style="max-width:238px; margin:1px"/>
    <img src="/assets/images/ss/Polaris_4.png" width=49%; style="max-width:238px; margin:1px"/>
    <img src="/assets/images/ss/Polaris_5.png" width=49%; style="max-width:238px; margin:1px"/>
    <img src="/assets/images/ss/Polaris_6.png" width=49%; style="max-width:238px; margin:1px"/>
</div>

## 개발 회고

### 면적에 비례한 캐릭터 출현 확률
"Polaris - The Story of Stars -"에서 가장 핵심이 되는 기능이라고 하면 단연 "관측 기능"이다.
관측 기능은 하단 UI의 제일 왼쪽 버튼을 눌러 접근 가능하며, 밤하늘의 원하는 위치에
망원경을 조준해 관측 지점을 설정하고, 시간을 들여 해당 지점을 관측해
관측 시간에 비례해 캐릭터와 캐릭터의 호감도를 얻는 기능이다.

언뜻 들으면 다른 게임의 이른바 "가챠" 기능과 크게 다를 바 없는 기능이지만, 관측 기능을
단순한 가챠와는 다르게 만드는 핵심 요소는 바로 관측 지점이 출현 확률에 영향을 끼친다는 것이다.
밤하늘에 묘사된 약 30여개의 별자리 각각마다 출현할 캐릭터와 그 비중이 설정되어 있고,
망원경이 "덮고 있는" 면적에서 각 별자리가 차지하는 비율이 추가로 반영되어 최종적으로 캐릭터의 출현 확률이 결정된다.

그런데, 망원경이 덮고 있는 원형의 지점에서 각 별자리가 얼마만큼의 자리를 차지하는지는 어떻게 알아내야 할까?
별자리마다 일종의 무게중심점이 있고 망원경의 중심으로부터의 거리를 활용해 비율을 계산하는 방법도 고려해 봤지만,
"그렇게 현실적이지 않을 것 같다", 즉 실제 비율을 반영하지 못할 것 같다는 의견이 팀 내부에서 제기되었다.

최종적으로 선택한 방법은 어찌 보면 굉장히 단순무식한 방법인데, 바로 **별자리 각각의 영역을 PolygonCollider2D로 정의하고,
망원경에서는 Raycast를 고르게 쏴, 별자리마다 각각 충돌한 Raycast의 개수를 그 비율로 한다**였다.

아래 코드는 ObserveManager 코드의 일부로, 현재 망원경의 위치에서 Raycast를 쏘는 코드이다.
```cs
public void ShotRay()
{
    var pos = Scope.transform.position;
    constelHitCount = constelHitCount.ToDictionary(p => p.Key, p => 0);

    CastRay(pos);
    CastRay(pos);
    CastRay(pos);
    CastRay(pos);

    for (int i = 1; i <= SCOPE_CIRCLE_COUNT; i++)
    {
        for (int j = 0; j < i * SCOPE_UNIT_RAYS; j++)
        {
            float r = SCOPE_RADIUS * (1f / SCOPE_CIRCLE_COUNT) * i;
            float theta = 2 * Mathf.PI * ((float)j / (SCOPE_UNIT_RAYS * i)) + (2 * Mathf.PI / SCOPE_UNIT_RAYS / SCOPE_CIRCLE_COUNT * (i - 1));
            pos = Scope.transform.position + new Vector3(r * Mathf.Cos(theta), r * Mathf.Sin(theta), 0);
            CastRay(pos);
        }
    }

    status.charProb.Clear();
    foreach(var constel in constelHitCount)
    {
        foreach(var charIndex in constelCharData[constel.Key].charas)
        {
            if (!status.charProb.ContainsKey(charIndex))
                status.charProb.Add(charIndex, 0);
            status.charProb[charIndex] += constel.Value * constelCharData[constel.Key].charWeights[charIndex];
        }
    }

    var centerConstel = GetCenterConstelKey();
    if (centerConstel == "null")
        ConstelName.text = "미지의 영역";
    else
        ConstelName.text = Variables.Constels[centerConstel].Name;
    ConstelImage.GetComponent<Image>().sprite = Resources.Load<Sprite>("Constellations/Observation/" + centerConstel);

    if (!status.isTutorial)
    {
        var orderedCharProb = status.charProb.OrderByDescending(p => p.Value);
        for (int i = 0; i < 4; i++)
        {
            if (i >= orderedCharProb.Count())
                CharDisplay[i].gameObject.SetActive(false);
            else
            {
                CharDisplay[i].gameObject.SetActive(true);
                CharDisplay[i].Set(orderedCharProb.ElementAt(i).Key);
            }
        }
    }
}
```
일단 중앙 지점의 낮은 확률을 보정하기 위해 Raycast를 4번 한 뒤, 중심으로부터 원을 그려 나가면서
각 원의 시작점도 비트는 등 최대한 균일하게 Raycast를 하려고 노력하였다. 그 다음 중앙 별자리의 정보를 가져오고,
Raycast를 하면서 수집한 캐릭터 확률 정보(CastRay 함수가 하는 일이다)를 정돈해 유저에게 보여준다.

개발 초기에는 "많은 게 좋은 거지" 하면서 쏘는 Ray의 개수를 매 프레임마다 약 10만 개 정도로 설정했었는데,
실제 디바이스에서 테스트할 때 성능 저하가 심하게 일어나 최종적으로는
망원경이 이동하고 있을 때에만 약 1천 개 정도를 쏘는 것으로 사양을 변경하였다.