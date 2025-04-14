<h1 id="게임오브젝트-gameobject">게임오브젝트 (GameObject)</h1>
<ul>
<li>씬을 구성하는 오브젝트이며 게임에 존재하는 모든 오브젝트는 게임오브젝트</li>
<li>씬에 존재하여 육안에 보이는 물체 또는 육안으로 보이지 않는 기능을 위한 구성품</li>
<li>게임오브젝트만으로는 독자적인 기능이 없음</li>
<li>실직적인 기능은 컴포넌트들이 수행</li>
<li>게임오브젝트는 컴포넌트들을 가지기 위한 컨테이너</li>
</ul>
<pre><code>    GameObject gameObj;</code></pre><h2 id="게임오브젝트-구성요소">게임오브젝트 구성요소</h2>
<ul>
<li>name         : 게임오브젝트의 이름</li>
<li>active       : 게임오브젝트의 활성화 여부, 비활성화인 경우 씬에 없는 게임오브젝트로 취급된다.</li>
<li>static       : 게임오브젝트의 정적상태 여부, 런타임 당시 변경되지 않는 데이터를 지정하여 최적화</li>
<li>tag          : 게임오브젝트의 태그, 게임오브젝트를 특정하기 위한 수단으로 사용</li>
<li>layer        : 게임오브젝트의 레이어, 씬에서 게임오브젝트를 분리하는 기준 (카메라의 선별적 표현, 충돌 그룹, 등)</li>
<li>component    : 게임오브젝트에 포함된 기능 모듈, 실질적인 기능을 수행</li>
</ul>
<h2 id="데이터-직렬화">데이터 직렬화</h2>
<ul>
<li>오브젝트의 멤버변수 값을 확인하거나 변경</li>
<li>오브젝트의 멤버변수 참조를 드래그 앤 드랍 방식으로 연결</li>
</ul>
<h3 id="직렬화-serialization">직렬화 (Serialization)</h3>
<ul>
<li>데이터 구조 또는 게임오브젝트 상태를 보관하고 관리하는 기법</li>
<li>인스펙터 창에서 오브젝트의 직렬화된 멤버변수 값을 보여준다.</li>
<li>이를 이용하여 소스코드의 수정 없이 유니티 에디터에서 값을 변경 가능하다.</li>
</ul>
<pre><code>[Header(&quot;Value&quot;)]

        // C# Type
        public bool boolValue;
        public int intValue;
        public float floatValue;
        public string stringValue;

        // Unity Type
        public Vector3 vector3;
        public Vector3Int vector3Int;
        public Vector2 vector2;
        public Vector2Int vector2Int;
        public Color color;
        public Rect rect;
        public LayerMask layerMask;
        public AnimationCurve curve;
        public Gradient gradient;

        // 열거형
        public ForceMode mode;

        // 직렬화 가능한 필드의 배열 및 List&lt;T&gt;
        public int[] array;
        public List&lt;int&gt; list;

        [Header(&quot;Reference&quot;)]
        // Object Type
        public new GameObject gameObject;
        public new Transform transform;
        public new Rigidbody rigidbody;
        public new Collider collider;



        어트리뷰트

        클래스, 속성 또는 함수 위에 명시하여 특별한 동작을 나타낼 수 있는 마커

        [Space(30)]

        [Header(&quot;Unity Attribute&quot;)]

        [SerializeField]
        private int privateValue;

        [HideInInspector]
        public int publicValue;

        [Range(0, 10)]
        public float rangeValue;

        [TextArea(3, 5)]
        public string textField;

        [Serializable] // 구조체에 직렬화 가능 속성을 포함
        public struct StructType
        {
            public int value1;
            public string value2;
        }
        public StructType structField;

        [Serializable] // 클래스에 직렬화 가능 속성을 포함
        public class ClassType
        {
            public int value1;
            public string value2;
        }
        public ClassType classField;</code></pre>