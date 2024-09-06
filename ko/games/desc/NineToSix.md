# Nine to Six

<div style="display:flex; flex-flow:row wrap-reverse;">
    <div style="display:flex; flex-flow:row wrap; min-width:50%; flex:1;">
        <md-block style="min-width:fit-content; padding-right:30px; flex:1;">
            ## 게임 정보
            - **장르**: 수강신청 액션
            - **플랫폼**: PC
            - **게임 엔진**: Unity
            - **개발 기간**: 2024. 1. (3일)
            - [GitHub에서 보기](https://github.com/2ndUNIJAM/NineToSix)
        </md-block>
        <md-block style="width:200px;">
            ## 다운로드
            <div style="width=100%; max-width:150px;">
                <a href="https://store.onstove.com/ko/games/3037" target="_blank">
                    <img src="/assets/images/icons/dlbadge_stove.svg" width=100%/>
                </a>
            </div>
        </md-block>
    </div>
    <div class="caption_img">
        <img src="/assets/images/NineToSix_banner.png" width=100%/>
        <p class="card_item_text">Nine to Six의 스토어 아이콘.</p>
    </div>
</div>

## 개요
엣말에 따르면 '시작이 반이다', 그리고 '가만히 있으면 중간은 간다'고 한다. 그렇다면 '시작하고 가만히 있으면' 목적지에는 이미 도달한 게 아닐까?
"Nine to Six"에서는 '시작하고 가만히 있기'를 신념으로 하는 대학생들의 수강신청을 학과 사무실 직원인 당신이 직접 해 줘야 한다.
학생들의 요구사항을 만족시키는 완벽하고 빠른 수강신청을 당신은 해낼 수 있을까?

## 제작 정보
"Nine to Six"는 약칭이며, 정식 명칭은 "Nine To Six : 태풍을 부르는 수강신청 타이쿤"이다.

본 작품은 [전국 게임 개발 동아리 연합회(UNIDEV)](https://unidev-page.notion.site/UNIDEV-06fff344b68748a29d5e7a1d05d7dd18)에서 주최한 게임잼 행사인 '제2회 UNIJAM'에 참여해 제작한 작품이다.

'제2회 UNIJAM'은 2024년 1월 26일(금)~2024년 1월 28일(일)의 3일간 개최되었으며,
참가자들은 총 48시간 동안 주어진 주제에 맞는 게임을 제작해야 했다.
한 팀은 5명으로 이루어졌으며, 직군은 다음과 같았다.

- 기획자 1명
- 메인 프로그래머 1명
- 서브 프로그래머 2명
- 아트 1명

본인은 메인 프로그래머로 참여하였다.

"Nine to Six" 는 제2회 UNIJAM에서 제작된 작품들 중 가장 좋은 평가를 받았다(대상 수상).
게임잼 종료 후 다른 참여작들과 함께 스토브 스토어에 게시되었다.

## 개발 회고

### 안전한 협업을 위한 노력
Unity를 이용해 여러 명이서 개발할 때, 작업을 공유하기 위해 주로 Git을 사용한다.
하지만 Unity와 Git의 상성이 그렇게까지 좋지는 않은데, 가장 대표적인 것이 씬과 프리팹 파일이다.
이 두 가지 파일은 텍스트 에디터를 통한 수정이 거의 불가능하기 때문에, 병합 충돌이 발생하면
두 버전 중 하나의 변경 사항은 포기해야 하는 문제가 생긴다.
이 때문에, Unity와 Git을 쓸 때 나는 가급적 하나의 씬, 프리팹은 한 사람만 만지도록 한다.
이 원칙을 세우고 지킨다면 적어도 씬과 프리팹이 병합 충돌을 겪을 일은 없기 때문이다.

하지만 게임잼에서는 원칙이고 자시고 일단 뭔가 빠르게 만들어야 한다.

"Nine To Six"를 기능별로 대략적으로 쪼개 보면 다음과 같다.

- 타이틀 화면
- 메인 게임
  - 학생 정보 표시
  - 과목 생성
  - 수강신청 액션

"Nine To Six"를 작업할 때, 나는 처음에는 위의 원칙을 지키면서 작업을 하려고 했다.
두 분의 서브 프로그래머에게 작업을 배분해야 했는데, 일단은 메인 기능(수강신청 기능)을 내가 구현하고,
나머지 기능들은 서브 프로그래머 분들이 구현하는 것으로 분배하였다.
이렇게 하면 각자가 각자의 씬을 맡기 때문에 작업이 꼬일 일이 없기 때문이다.

하지만 이 게임의 복잡한 기능이 수강신청 액션 파트에 집중되어 있기 때문에,
48시간의 짧은 기간 동안 혼자서 해당 파트의 모든 기능을 구현하는 것은 힘들었다.

(추가 작성 예정)s