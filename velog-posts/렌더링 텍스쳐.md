<h1 id="개요">개요</h1>
<p>CCTV를 게임에 구현하조자 하려면</p>
<p>보조 카메라가 보고 있는 곳을 한 장의 이미지로 표현한다면 구현이 가능할 것 같습니다.</p>
<p>이를 실현 가능하게 해주는 렌더링 텍스쳐에 대해 알아볼수있다.</p>
<h1 id="렌더링-텍스쳐">렌더링 텍스쳐</h1>
<p>카메라가 렌더링하는 화면을 실시간으로 보는 것 뿐만 아니라 보조 카메라가 렌더링하는 화면을 추가로 다루고 싶을 때 렌더링 텍스쳐를 사용합니다.</p>
<p>이는 렌더링 결과물을 텍스쳐 형태로 저장하는 용도로 사용되는</p>
<h1 id="텍스쳐texture란">텍스쳐(Texture)란?</h1>
<p>텍스쳐는 도형의 전개도와 같습니다. 우리는 예쁘게 색칠된 정육면체의 전개도를 실제 크기가 같은 정육면체의 표면에 맞춰 붙일 수 있습니다.</p>
<p>텍스쳐는 이와 같이 모델이 가지고 있는 꼭지점(버텍스)의 위치(텍스쳐 좌표 u, v) 매칭(매핑)되는 전개도이며, 이는 2D 이미지로 구성됩니다.</p>
<p>렌더링 텍스쳐는 말 그대로 렌더링 되고 있는 화면을 텍스쳐 형태로 저장한 것입니다.</p>
<p>렌더링 텍스쳐는 게임 최적화 요소로도 쓰이며, 대표적인 예시로 자연 효과(물)등을 실시간으로 연산할 시 생기는 부하를 방지하기 위해 미리 물이 흐르는 영상을 미리 녹화해두는 방식으로 구현됩니다.</p>
<p>또한 거울, 그림자, 광원, 화면 캡쳐의 목적 등 게임에서 발생하는 실시간 연산을 줄이기 위한 수단으로 활용되므로, 사용법을 알고 있다면 게임 최적화 수단으로도 활용될 수 있는 유용한 요소입니다.</p>
<h1 id="rendertexture-에디터에서-생성-및-연결하는-법">RenderTexture 에디터에서 생성 및 연결하는 법</h1>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/0a3ba046-49c2-4d57-ab7e-7d916a3063df/image.png" /></p>
<p>Project 창에서 빈 곳에 우클릭</p>
<p>Create → Render Texture 선택</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/0842b000-165b-4400-99a4-c7860a8da9f1/image.png" /></p>
<p>Scene 내 Camera 선택</p>
<p>Inspector에서 Target Texture 항목 클릭</p>
<p>MyRenderTexture 드래그해서 넣기</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/a9728bf7-ee38-4013-93ff-41f4e0870525/image.png" /></p>
<p>Canvas 생성 → RawImage 추가</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/bfc53904-7aad-4eb5-86aa-8cc03818297d/image.png" /></p>
<p>RawImage의 Texture 항목에 MyRenderTexture를 드래그해서 넣기</p>
<h3 id="cctv의-경우">CCTV의 경우</h3>
<p><img alt="업로드중.." src="blob:https://velog.io/5823dc74-fcee-4f6e-a24f-e72aad0b3e5c" /></p>