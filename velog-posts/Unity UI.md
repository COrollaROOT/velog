<h1 id="개요">개요</h1>
<p>UI는 게임의 사용자가 게임에 가장 직접적으로 마주하는 첫 번째 상호작용 요소이다.</p>
<p>게임을 떠나 어떤 프로그램이든 UI가 존재하고, 사용자는 UI를 가장 먼저 마주한다.</p>
<p>유니티에서 UI가 생성될 때 어떤 요소로 구성되어 있고,</p>
<p>이를 적은 연산으로 최대의 효율을 낼 수 있는지 알아볼수 있다.</p>
<h1 id="게임-ui">게임 UI</h1>
<ul>
<li><p>UI는 User Interface의 줄임말로, 사용자에게 제공되는 프로그램으로의 가장 직관적인 접근 요소입니다.</p>
</li>
<li><p>유저는 UI를 통해 프로그램으로부터 원하는 결과를 얻는 데 사용합니다.</p>
</li>
<li><p>UI는 사용 환경에 따라 다양한 해상도에 유연하게 적용되어야 하며, 이는 UI를 구성함에 있어 가장 중요한 핵심 요소중 하나입니다.</p>
</li>
<li><p>실제로 게임에서 UI의 구조를 효과적으로 설계하고 적용하는 것은 생각보다 어려운 일이며 추후 프로그램의 유지보수, 업데이트와 같은 확장성을 고려한 객체지향적 설계가 적용되어야 할 중요한 요소입니다.</p>
</li>
</ul>
<h2 id="ui-구성요소">UI 구성요소</h2>
<ul>
<li><p>UI는 반드시 Canvas라는 오브젝트에 포함되어 있어야 하며 Canvas는 UI를 배치하는 평면의 도화지입니다.</p>
</li>
<li><p>Canvas와 모든 UI는 일반 3D 오브젝트와는 다르게 UI를 화면에 표기하기 위한 2차원 사각형 내의 위치를 제어하기 위한 RectTransform 컴포넌트가 포함되어 있습니다.</p>
</li>
<li><p>RectTransform은 해상도 변경시에도 부모 오브젝트의 위치에 고정하고 위치를 정렬하기 위한 앵커와 회전의 기준점이 되는 피벗을 가지고 있습니다.</p>
</li>
</ul>
<h2 id="ngui--ugui">NGUI / UGUI</h2>
<ul>
<li><p>NGUI와 UGUI 모두 유니티에서 사용하는 UI 시스템이지만, 둘은 다른 특성을 가집니다</p>
</li>
<li><ul>
<li>NGUI는 패키지를 다운로드 후 사용합니다. 커스터마이징을 위해 많은 작업을 필요로 하며, 상대적으로 적은 성능을 요구하기에 경량화된 성능을 요구하는 프로젝트에서 사용하기 적합합니다.</li>
</ul>
</li>
</ul>
<ul>
<li><ul>
<li>UGUI는 유니티의 렌더링 파이프라인에 통합되어 있으며, 구성요소도 게임오브젝트와 같은 방식으로 처리됩니다. 별도의 컨트롤창이 아닌 하이어라키에서 직관적으로 편집할 수 있습니다.</li>
</ul>
</li>
</ul>
<h2 id="anchor-pivot">Anchor, Pivot</h2>
<ul>
<li><p>앵커와 피벗은 UI를 정렬 및 위치 조정에서 중요한 역할을 합니다. 게임들은 여러 해상도에서도 모든 UI를 일관성있게 배치하는 모습을 보여줍니다. 유니티에서는 이를 앵커와 피벗으로 구현할 수 있습니다</p>
</li>
<li><ul>
<li>Anchor : UI 요소가 부모 UI오브젝트에 대한 상대좌표를 정의합니다. 이를 사용하면 UI 요소가 화면 크기가 변해도 같은 위치에 있도록 설정할 수 있습니다.</li>
</ul>
</li>
</ul>
<ul>
<li><ul>
<li>Pivot : 자신 UI 오브젝트의 회전이나 크기 조정시 로컬 공간 내의 하나의 기준점입니다. (0, 0)은 왼쪽 하단, (1, 1)은 오른쪽 상단을 의미합니다.</li>
</ul>
</li>
</ul>
<h1 id="기본-지원-ui">기본 지원 UI</h1>
<h2 id="image--raw-image">Image / Raw Image</h2>
<ul>
<li><p>Raw Image는 원본 이미지를 그대로 출력하기 때문에 이미지에 대한 추가 처리가 필요하지 않아 처리 속도가 빠르고 주로 동영상 재생에 적합합니다.</p>
</li>
<li><p>Image는 Sprite와 Color 데이터를 통해 이미지를 출력하기 때문에 렌더링 전 발생하는 전처리 과정으로 상황에 따라 처리 비용이 높을 수 있습니다.</p>
</li>
</ul>
<h2 id="button">Button</h2>
<p>마우스 클릭 / 화면 터치를 위한 UI 구성요소입니다. 내부적으로 클릭 시 동작을 정의할 수 있도록 OnClick 이벤트를 내장하고 있으며, 이벤트 트리거를 사용해 다양한 구현이 가능합니다.</p>
<h2 id="slider">Slider</h2>
<p>주로 옵션 창에서 볼륨 설정 등에 사용됩니다. 마우스 혹은 터치 드래그를 통해 값을 조절합니다.</p>
<p>변경되는 값은 0 에서 1까지의 소수입니다</p>
<h2 id="scroll-view">Scroll View</h2>
<p>한정된 영역에 많은 데이터를 넣을 때 사용합니다. 스크롤바를 통해 영역을 이동하며 데이터를 열람할 때 사용하며, 모바일 플랫폼을 위한 터치 및 반동 기능도 지원합니다.</p>
<h2 id="textmeshpro">TextMeshPro</h2>
<p>UI에 빠질 수 없는 요소중 하나는 Text입니다.</p>
<p>유니티에서는 기본적인 Text 외에도 여러 확장기능을 포함한 TextMeshPro를 기본적으로 지원합니다.</p>
<p>TextMeshPro는 예전 버전에서는 유료 기능이었지만, 현재는 무료 기능입니다.</p>
<p>유니티에서는 기본적으로 한글 폰트를 지원하지 않기 때문에 특수한 과정을 거쳐 '폰트 에셋'을 생성해야 합니다.</p>
<h1 id="unity-한글-폰트-설정-하는법">Unity 한글 폰트 설정 하는법</h1>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/462b5ffc-0dae-4489-a567-fdba89290ed9/image.png" /><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/bd1280d6-af3f-44af-9a61-77a12106fdca/image.png" /></p>
<p>먼저 한글을 지원하는 무료 폰트를 다운 받아 준다</p>
<p>!!!저작권 주의!!!</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/caa9da50-ddbd-47e2-8139-d3830f5af335/image.png" /></p>
<p>다운 받은 폰트를 Unity에 포함 시킨다(끌어다 넣어주면 끝!)</p>
<p>하지만 바로 사용 할수는 없다</p>
<p>폰트를 이미지화 하여 쓸수 있기 때문에 폰트를 폰트에셋으로 설정해 주어야 한다</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/7f492aeb-bc98-4e1d-bad3-877fb8a39f8c/image.png" /></p>
<p>Window -&gt; TextMeshPro -&gt; Font Asset Creator 선택</p>
<p>Text Asset 생성
<img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/5d750106-ade9-40ba-9c40-11da122522a3/image.png" /></p>
<ol>
<li>Source Font File : 폰트 원본 파일 삽입</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/b2a543be-f391-4ffd-8091-d5cd88792100/image.png" /></p>
<ol start="2">
<li>Sampling Point Size : 텍스쳐화 될 폰트 이미지에 삽입될 글자의 크기, 일반적으로 Auto Sizing을 선택한다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/cbbdf57d-2047-4dd6-b8ff-1a98dd9b534b/image.png" /></p>
<ol start="3">
<li>Padding : 글자 이미지 간의 여백, 보통 5를 선택한다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/f73640aa-97f5-42b1-9611-daa7e914c821/image.png" /></p>
<ol start="4">
<li>Packing Method : 폰트들을 한 장의 이미지로 합쳐 아틀라스를 생성한다. 두 옵션의 차이가 크지 않으므로 'Fast'를 선택한다</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/57b01be6-75a8-48fc-8795-88e0d1531d9f/image.png" /></p>
<ol start="5">
<li>Atlas Resolution : 글자로 구성된 한 장의 이미지의 최대 크기, 너무 작다면 폰트가 제대로 출력되지 않을 수 있고 너무 크다면 성능적으로 좋지 않다. 한글이라면 일반적으로 2048 ~ 4096을 추천한다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/d14716a4-1a7b-4417-b726-a0b31f4961e1/image.png" /></p>
<ol start="6">
<li>Character Set : 폰트에셋으로 지정해 둘 폰트를 지정하는 단계. 한글폰트가 포함되어야 하므로 Custom Range로 설정한다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/272d6950-3c56-4bd7-9167-74c3775ce46b/image.png" /></p>
<ol start="7">
<li>Character Sequence : 유니코드 단위의 10진수로 범위를 지정한다. 32-126,44032-55203,12593-12643,8200-9900를 입력하며. 이는 각각 영문자, 한글, 한글 자모음, 특수문자의 범위이다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/a8f0e586-a509-4349-b87e-3a0f6e58c685/image.png" /></p>
<ol start="8">
<li>RenderMode : 텍스트를 이미지화 할 때 사용되는 렌더링 모드. 거리에 따라 선명도를 계산해 렌더링 하는 방식인 SDF를 사용하고, 그 중에서도 SDF16 을 선택하지만 이 수치는 디바이스 환경이나 해상도 등에 차이가 있을 수 있으며 숫자가 높을수록 더 많은 연산이 발생하므로 많은 테스트를 통해 결정되어야 한다.</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/24f85775-7ea2-4b48-ad4f-c6749a8f4438/image.png" /></p>
<p>Generate Font Atlas 누르면 폰트가 생성 되고
Save 눌러 저장 하면 폰트가 완성된다</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/5619eae2-af4e-4a3b-8ed0-e805235ee3f9/image.png" /></p>
<p>이제 완성된 폰트를 Text창 Font Asset에 적용하면 한글이 깨져 보이던게 제대로 출력되는것을 볼수 있다</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/4223c0c0-25d7-468f-b61c-6b049930ff62/image.png" /></p>