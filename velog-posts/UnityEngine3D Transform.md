<h1 id="transform-component">Transform Component</h1>
<p>트랜스폼 (Transform)</p>
<p>게임오브젝트의 위치, 회전, 크기를 저장하는 컴포넌트
게임오브젝트의 부모 - 자식 상태를 저장하는 컴포넌트
게임오브젝트는 반드시 하나의 트랜스폼 컴포넌트를 가지고 있으며 추가 &amp; 제거할 수 없음</p>
<h2 id="position">Position</h2>
<p>유니티에서 오브젝트의 위치 정보는 x, y, z 3축으로 구성됩니다. 이는 유니티에서 Vector3 클래스를 통해 간편하게 다룰 수 있으며, 이를 사용해 게임 오브젝트의 위치 이동을 구현할 수 있습니다.</p>
<pre><code>// Position을 직접적으로 변경하는 방법
Transform.position = new Vector3(x, y, z);

// Translate 함수를 이용한 축(x, y, z) 기준의 위치이동 방법
Transform.Translate(Direction * Speed);

// 선형 보간을 이용해 거리에 따라 빠르게 이동하며 천천히 감속하는 방법
Transform.position = Vector3.Lerp(StartPosition, EndPosition, Interpolation)

// 목표지점을 향해 일정한 속도로 이동하는 방법
Transform.position = Vector3.MoveTowards(transform.position, Target.Position, Speed);</code></pre><h2 id="rotation">Rotation</h2>
<p>인스펙터의 Transform 컴포넌트에서는 회전값이 포지션과 동일하게 x, y, z축으로 보여지지만 내부 동작은 4원소를 사용하는 쿼터니언을 통해 이뤄집니다. 이는 연산속도가 빠르고 3축을 사용했을 때의 짐벌락 현상을 방지하는 데 효과적입니다.
쿼터니언은 연산적으로 효과적이지만, 유니티 입문 시점에서는 이해하기 복잡한 개념입니다. 이 때문에 보다 직관적인 3축으로 컨트롤 할 수 있도록 Quaternion클래스의 Euler를 사용합니다.</p>
<pre><code>// rotation에 값을 직접 지정해 회전하는 방법
Transform.rotation = Quaternion.Euler(x, y, z);

// Rotate 함수를 이용한 회전
Transform.Rotate(Vector3.up, Speed);

// RotateAround를 이용한 중심축 기준으로 회전
Transform.RotateAround(Target.position, Vector3.up, Speed);

// LookAt을 이용한 대상을 향해 회전시키기
Transform.LookAt(Target.position);</code></pre><h2 id="quaternion">Quaternion</h2>
<p>유니티 Transform에서 보여지는 오릴러 각(x, y, z축)이 아닌 4개의 실수로 구성된 복소수로 오브젝트의 회전을 연산합니다.
오일러 각을 기반으로 회전에 대한 연산을 다루지 않는 이유는 두개의 축이 겹쳐져 하나의 축이 기능을 상실하는 '짐벌락 현상'을 방지할 수 있고, 성능적으로 오일러 각보다 연산 성능적으로 우수하기 때문입니다. 이러한 이유로 유니티엔진 내부적으로 회전에 대한 연산은 쿼터니언을 사용해 구현되었습니다.</p>
<ul>
<li>짐벌락 현상</li>
</ul>
<h2 id="scale">Scale</h2>
<p>직관적인 이름 그대로 게임 오브젝트의 크기를 비율로 지정할 수 있는 요소입니다</p>
<pre><code>// Scale 조절
Transform.localScale = new Vector3(x, y, z);

// lossyScale은 부모 오브젝트의 스케일에 상관 없이 자신 고유의 Scale 수치를 반환
Transform.lossyScale</code></pre><h1 id="프레임frame">프레임(Frame)</h1>
<p>1프레임당 걸린시간 = 단위시간
Frame / 1 = </p>