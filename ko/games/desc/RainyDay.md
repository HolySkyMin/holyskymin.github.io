# Rainy Day Walker

<img src="/assets/images/RainyDay_banner.png" width=100%>

<div style="display:flex; flex-flow:row wrap;">
    <md-block style="min-width:fit-content; max-width:570px; padding-right:30px; flex:1">
        ## 게임 정보
        - **장르**: 걷기 게임, 스토리텔링
        - **플랫폼**: PC
        - **게임 엔진**: Unity 2021.3
        - **개발 기간**: 2023. 1. ~ 2023. 2. (2개월)
    </md-block>
    <md-block style="width:250px;">
        ## 다운로드
        <div style="width=100%; max-width:250px;">
            <a href="https://holysky.itch.io/rainy-day-walker" target="_blank" style="text-decoration:none;">
                <img src="/assets/images/icons/dlbadge_itch.svg" width=100%/>
            </a>
        </div>
    </md-block>
</div>

## 개요
"Rainy Day Walker"는 스토리텔링 요소가 가미된 걷기 게임이다. 신발이 물에 젖지 않도록 물웅덩이를 피하면서 길을 걸어나가자.
그런데, 어째서 이 사람은 비 오는 거리를 한없이 걷고 있는 걸까? 아마도, 게임을 진행해 나가다 보면,
그가 느꼈던 절망과 K-Pop의 어두운 일면을 알게 될 지도 모른다.

## 제작 정보
"Rainy Day Walker"는 서울대학교 게임개발동아리(SNUGDC) 내부 활동을 통해 제작되었으며,
2023년 NDM(Nexon Dream Members)에 출품하였다.

제작 인원은 총 3명이며, 인원 구성은 다음과 같다.

- 기획 및 프로그래밍 1명
- 2D 아트 1명
- 3D 아트 1명

본인은 본 작품의 기획과 프로그래밍을 맡았다.

게임을 제작하면서 환경 모델링에 유료 에셋을 활용하였기 떄문에 프로젝트 전체를 공개할 수 없다.
소스 코드의 공개에 대해서는 다른 방법을 고려해 볼 예정이다.

## 스크린샷
<img src="/assets/images/RainyDay_image.png" width=100%/>

## 개발 회고

### 비에 젖은 땅
"Rainy Day Walker"의 핵심 플레이 기믹은 물웅덩이를 피하며 길을 걷는 것인데,
여기에서 가장 큰 문제가 된 것은 바로 물웅덩이를 생성하는 것이었다.
물웅덩이를 미리 배치할 수 있는 스토리 모드에서는 큰 문제까지는 아니지만, 계속해서 길을 생성해야 하는
무한 모드에서는 물웅덩이 역시 무작위로 배치해야 하는 문제가 있었다.
또한, 물웅덩이를 프리팹으로 배치한다고 하면 무엇보다도 다양해야 하는 물웅덩이의 모양이 작업량으로 발목을 잡는다.

"Rainy Day Walker"에서 선택한 방법은 Perlin Noise를 활용해 지형을 생성하는 것이다.
길을 만들기 위해, 우선 물의 역할을 할 평면 메시를 배치하고, 땅보다 밝게 표현되도록 색상을 조절한다.
그 다음 땅의 역할을 할 메시를 만드는데, 이 때 정점(Vertex)을 2차원 평면처럼 놓은 뒤
각 정점의 높이를 결정하는 변수로 Perlin Noise를 활용했다.
이를 통해 자연스러움을 어느 정도 포기하는 대신, 작업량이 획기적으로 줄어들었고 무작위 생성 역시 가능해졌다.

아래 코드는 물웅덩이가 있는 길을 나타내는 컴포넌트인 GeneratableField 클래스의 일부이다.
```cs
public void GenerateField(int width, int length, int waterLevel, float noiseDensity, float seedX, float seedZ)
{
    if (reverseWaterLevel)
        waterLevel = 100 - waterLevel;
    
    _mesh = new Mesh()
    {
        name = "Walking Terrain"
    };
    GetComponent<MeshFilter>().mesh = _mesh;

    // Creating Mesh Shape
    _vertices = new Vector3[(width + 1) * (length + 1)];
    _uvs = new Vector2[(width + 1) * (length + 1)];

    var minSize = Mathf.Min(width, length);
    for(int i = 0, z = 0; z <= width; z++)
    {
        for(int x = 0; x <= length; x++, i++)
        {
            var y = MAX_HEIGHT * Mathf.Clamp01(Mathf.PerlinNoise(x * noiseDensity / minSize + seedX, z * noiseDensity / minSize + seedZ));
            _vertices[i] = new Vector3(x, y, z);
            _uvs[i] = new Vector2(x * tileSize / minSize, z * tileSize / minSize);
        }
    }
    
    _triangles = new int[width * length * 6];
    for(int z = 0, vert = 0, tris = 0; z < width; z++, vert++)
    {
        for(int x = 0; x < length; x++, vert++, tris += 6)
        {
            _triangles[tris] = vert;
            _triangles[tris + 1] = vert + length + 1;
            _triangles[tris + 2] = vert + 1;
            _triangles[tris + 3] = vert + 1;
            _triangles[tris + 4] = vert + length + 1;
            _triangles[tris + 5] = vert + length + 2;
        }
    }

    // Updating Mesh Data
    _mesh.Clear();

    _mesh.vertices = _vertices;
    _mesh.triangles = _triangles;
    _mesh.uv = _uvs;

    _mesh.RecalculateNormals();
    _mesh.RecalculateBounds();

    GetComponent<MeshCollider>().sharedMesh = _mesh;

    // Configuring Water Object
    if (stretchWaterObject)
    {
        waterObject.transform.localPosition = new Vector3(length / 2f, MAX_HEIGHT * waterLevel / 100f, width / 2f);
        waterObject.transform.localScale = new Vector3(length / 10f, 0.0001f, width / 10f);
    }
    else
        waterObject.transform.localPosition = new Vector3(
            waterObject.transform.localPosition.x,
            MAX_HEIGHT * waterLevel / 100,
            waterObject.transform.localPosition.z
        );
    waterObject.SetActive(true);
}
```