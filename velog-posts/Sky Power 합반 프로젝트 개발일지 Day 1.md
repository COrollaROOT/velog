<p>본격적인 프로그램 개발전에 UML다이어그램을 사용하여 각자가 맡은 파트의 주요 기능을 재정비 하는 시간을 가졌습니다</p>
<p>이번 프로젝트를 하면서 UML다이어그램을 처음 써보기에</p>
<p>이렇게 TIL을 작성하여 왜 필요한지 어떻게 써야하는지 알아보겠습니다</p>
<h1 id="uml다이어그램">UML다이어그램</h1>
<ul>
<li><p>UML (통합 모델링 언어)는 소프트웨어 및 시스템 개발에서 사용되는 표준화된 모델링 언어입니다.</p>
</li>
<li><p>시스템의 구조, 동작, 상호 작용 등을 시각적으로 표현하여 개발자, 설계자, 관리자 간의 의사소통을 원활하게 하고 시스템의 이해도를 높이는 데 사용됩니다.</p>
</li>
</ul>
<h2 id="uml다이어그램의-주요-특징">UML다이어그램의 주요 특징</h2>
<ul>
<li><p>표준화 : OMG(Object Management Group)에서 표준화한 언어입니다. </p>
</li>
<li><p>시각적 표현 : 다이어그램을 사용하여 시스템의 다양한 측면을 그림으로 나타냅니다. </p>
</li>
<li><p>다양한 다이어그램 : 시스템의 구조, 동작, 상호 작용 등을 표현하기 위한 여러 종류의 다이어그램을 제공합니다.</p>
</li>
<li><p>의사소통 도구 : 개발자, 설계자, 관리자, 기획자 등 다양한 이해 관계자 간의 의사소통을 돕습니다. </p>
</li>
<li><p>유연성 : 다양한 개발 방법론 및 프로그래밍 언어와 함께 사용될 수 있습니다. </p>
</li>
</ul>
<h2 id="주요-종류">주요 종류</h2>
<h4 id="구조-다이어그램">구조 다이어그램:</h4>
<ul>
<li><p>클래스 다이어그램: 시스템의 클래스, 속성, 메서드, 관계 등을 표현합니다. </p>
</li>
<li><p>객체 다이어그램: 특정 시점의 객체 상태를 표현합니다. </p>
</li>
<li><p>컴포넌트 다이어그램: 시스템의 물리적 컴포넌트와 그 관계를 표현합니다. </p>
</li>
<li><p>배포 다이어그램: 시스템의 하드웨어 및 소프트웨어 배포 구조를 표현합니다. </p>
</li>
<li><p>패키지 다이어그램: 시스템의 논리적인 그룹화 (패키지) 및 관계를 표현합니다.</p>
</li>
</ul>
<h4 id="행동-다이어그램">행동 다이어그램:</h4>
<ul>
<li><p>유스케이스 다이어그램: 사용자와 시스템 간의 상호 작용을 표현합니다. </p>
</li>
<li><p>시퀀스 다이어그램: 객체 간의 시간 순서에 따른 메시지 교환을 표현합니다. </p>
</li>
<li><p>활동 다이어그램: 시스템의 동작 흐름이나 비즈니스 프로세스를 표현합니다. </p>
</li>
<li><p>상태 다이어그램: 객체의 상태 변화와 이벤트를 표현합니다. </p>
</li>
<li><p>커뮤니케이션 다이어그램: 객체 간의 상호 작용을 표현합니다. (시퀀스 다이어그램과 유사) </p>
</li>
<li><p>상호 작용 개요 다이어그램: 상호 작용 다이어그램의 흐름을 개요 수준에서 표현합니다. </p>
</li>
<li><p>타이밍 다이어그램: 시간 제약 조건이 있는 객체 간의 상호 작용을 표현합니다. </p>
</li>
</ul>
<h2 id="uml의-활용">UML의 활용</h2>
<ul>
<li><p>시스템 설계: 시스템의 구조와 동작을 설계하고 문서화합니다. </p>
</li>
<li><p>요구사항 적용: 협업자의 요구사항을 바로 반영할 수 있습니다. </p>
</li>
<li><p>프로젝트 관리: 프로젝트의 진행 상황을 시각적으로 관리하고 의사소통합니다.</p>
</li>
</ul>
<hr />
<p>여기까진 UML 다이어그램의 기본 지식을 알아 보았습니다</p>
<p>다음으론 개발자가 UML 다이어그램을 더욱 더 
효율적으로 쓸수있도록 자세히 알아 보겠습니다</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/ad2eae96-ed6a-47bb-90e3-45f1092edc88/image.png" /></p>
<p>클래스 다이어그램의 목적에 따라 개념 - 명세 - 구현 단계로 나눌 수 있습니다</p>
<p>개념 단계에서는 클래스만 도출하고 관계를 단순화하는 것이 목적입니다</p>
<p>명세와 구현 단계에서는 개발 직전 설계나 구현 이후 설명 목적으로 사용하고</p>
<p>UML 다이어그램을 기반으로 코드로 구현하거나 코드를 기반으로 UML 다이어그램을 작성할 수 도 있기 때문에 코드와 연관이 깊습니다</p>
<p>UML 다이어그램을 구성하는 요소들을 알아 보겠습니다</p>
<h1 id="class">Class</h1>
<ul>
<li>개발자가 제일 많이 쓰게 될 클래스 다이어그램에서 클래스는</li>
<li><ul>
<li>이름, 속성(변수), 메소드 순으로 나열 합니다</li>
</ul>
</li>
<li><ul>
<li>속성과 메소드는 생략이 가능 하나 반드시 이름은 존재 해야 합니다</li>
</ul>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/78f32ceb-b07b-4bb9-83a8-3ebbb198f23f/image.png" /></p>
<p>다이어그램 클래스 앞에 붙는</p>
<p>(+)는 public (-)는 private (#) protected (~) default 을 의미 합니다</p>
<p>{readonily} 가 붙으면 final을 밑줄은 static을 의미합니다</p>
<ul>
<li>List는 사이즈가 정해지지 않아서 [*] 로 표기</li>
<li>Optional의 경우, 0 OR 1 이여서 [0..1] 로 표기</li>
<li>리스트와 같은 변수에 지정된 사이즈를 뜻합니다</li>
<li>Array와 같이 미리 사이즈를 지정한다면 [5] 와 같이 표기 가능</li>
</ul>
<p>이러한 의미는 속성과 메소드 둘 다 사용하여 표기 가능합니다</p>
<p>속성(변수)를 보면 접근 제어자, 필드명, 타입 순으로 작성 합니다</p>
<ul>
<li><p>{접근제어자}{필드명}{타입}</p>
</li>
<li><ul>
<li>메소드는 접근제어자, 메소드명(파라미터 타입), 반환 타입 순으로 작성</li>
</ul>
</li>
<li><p>{접근제어자}{메소드명}({파라미터타입}): {반환타입}</p>
</li>
</ul>
<h1 id="스테레오-타입">스테레오 타입</h1>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/2d910cfa-b078-4984-9cec-1ed29eee1431/image.png" /></p>
<p>인터페이스나 추상 클래스와 같은 요소를 표기 하기위해 &lt;&lt;길러멧(guillemet)&gt;&gt; 와 같은 문법을 사용합니다</p>
<ul>
<li>길러멧은 클래스명 위에 작은 글씨로 작성</li>
<li>길러멧은 보통 인터페이스,enum,추상 클래스 등에서 사용</li>
<li>사용자의 확장 클래스를 의미</li>
</ul>
<h1 id="추상-클래스">추상 클래스</h1>
<p>추상 클래스를 나타내는 방법</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/9a7d9e20-ab2c-4c47-ab43-d8580e9129b5/image.png" /></p>
<h1 id="클래스-간-관계">클래스 간 관계</h1>
<p>클래스 간 관계를 정확히 하는 것이 클래스 다이어그램을 사용하는 주된 목적 입니다</p>
<p> <img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/40dd4ae5-6b61-4f4b-a937-f3fc77bdd09f/image.png" /></p>
<h2 id="association">Association</h2>
<p>다른 객체의 참조를 가지고 있을 때 연관 관계를 나타냅니다</p>
<p>아래처럼 두 가지로 연관 관계를 나타낼 수 있습니다</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/ee9ac696-58eb-49b3-ba99-88c484f0f664/image.png" /></p>
<ul>
<li>A → B 방향이 있는 실선 (A가 B를 참조한다)</li>
<li>A - B 방향이 없는 실선 (B가 A를 참조 || 둘 다 참조 || !둘 다 참조)</li>
</ul>
<h2 id="inheritance">Inheritance</h2>
<p>상속 관계를 나타냅니다 Generalization - 일반화
부모 클래스와 자식 클래스 간의 상속관계를 나타낼때 사용</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/ad2eae96-ed6a-47bb-90e3-45f1092edc88/image.png" /></p>
<h2 id="realization">Realization</h2>
<p>인터페이스를 상속 클래스에서 실제 기능을 실현화 할 때 사용</p>
<p>아래처럼 두 가지로 표시 가능 합니다</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/fec063b7-a166-4f1b-bdb7-7e3e5ee96c47/image.png" /></p>
<h2 id="dependency">Dependency</h2>
<p>클래스간 참조 관계를 나타낼때 사용</p>
<ul>
<li><p>Association과의 차이점은 Association은 변수로 다른 클래스와 연관이 있을때 사용</p>
</li>
<li><p>Dependency는 메소드의 파라미터나 반환에 사용되는 클래스 관계를 나타낼 때 사용</p>
</li>
<li><ul>
<li>Association 관계는 해당 클래스의 멤버 변수로 할당할 때 사용</li>
</ul>
</li>
<li><ul>
<li>Dependency 관계는 로컬 변수, 파라미터, 반환 값으로 호출되는 메소드가 실행되는 동안에만 유지</li>
</ul>
</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/4d5a0e87-3c05-41ef-b64e-00f021d118e7/image.png" /></p>
<h2 id="aggregation">Aggregation</h2>
<p>집합 관계를 나타낼 때 사용</p>
<p>전체와 부분의 관계를 나타내지만, 부분은 전체와 독립적으로 존재할 수 있습니다. </p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/7971a745-e346-47c0-ae83-6bf4abdadc67/image.png" /></p>
<p>예를 들어, &quot;자동차&quot;와 &quot;바퀴&quot;의 관계처럼 전체가 사라져도 부분은 존재할 수 있습니다. 빈 다이아몬드 모양으로 표현합니다</p>
<h2 id="composition">Composition</h2>
<p>합성 관계를 나타낼 때 사용</p>
<p>집합 관계와 유사하지만, 전체와 부분이 강하게 결합되어 전체가 사라지면 부분도 함께 사라지는 관계입니다. </p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/4a727685-0a9b-47b3-a4e1-dd087c8cfe2c/image.png" /></p>
<p>예를 들어, &quot;컴퓨터&quot;와 &quot;본체&quot;의 관계처럼 전체가 없으면 부분도 존재할 수 없습니다. 속이 채워진 다이아몬드 모양으로 표현합니다. </p>