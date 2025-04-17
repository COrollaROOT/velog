<h1 id="rigidbody">Rigidbody</h1>
<ul>
<li><p>컴포넌트는 게임 오브젝트에 물리엔진을 적용하는 컴포넌트입니다.</p>
</li>
<li><p>물체의 질량, 공기저항, 중력에 대한 연산과 기본지원 함수를 사용해 보다 현실적인 물리처리가 가능합니다.</p>
</li>
<li><p>Rigidbody에서 지원되는 함수</p>
</li>
<li><p>-AddForce(x, y, z)
매개변수로 입력되는 x, y, z축 방향으로 물리적인 힘을 가합니다. 입력이 반복될수록 적용되는 힘이 누적됩니다.</p>
</li>
<li><p>-AddTorque()
매개변수로 입력되는 축의 물리적인 회전력을 더합니다.</p>
</li>
<li><p>-velocity
게임 오브젝트에 가해지고 있는 물리력입니다.</p>
</li>
<li><p>-angularVelocity
게임 오브젝트에 가해지고 있는 회전력입니다.</p>
</li>
</ul>
<p>Rigidbody 컴포넌트
Mass : 무게
Drag : 저항</p>
<pre><code>private void Update()
{
    float x = Input.GetAxis(&quot;Horizontal&quot;)
}

private void FixedUpdate()
{
    // 힘 가해주기 : 가속 시키기
    rigid.AddForce(Vector3.right * xInput * power, ForceMode.Force);

     // 속도를 설정 : 속도를 원하는대로 설정
    rigid.velocity = Vector3.right * power * xInput;

    // 회전력 가해주기
    rigid.AddTorque(Vector3.up * xInput * power);

    // 회전속도 설정
    rigid.angularVelocity = Vector3.up * power * xInput;
}</code></pre><h1 id="충돌처리">충돌처리</h1>
<p>충돌처리는 Rigidbody와 Collider를 통해 이뤄집니다.</p>
<p>상황에 따라 IsTrigger 사용 여부를 선택하고 Collision과 Trigger로 사용합니다.</p>
<h2 id="collision">Collision</h2>
<p>게임오브젝트의 물리적 충돌을 목적으로 모양을 정의
게임오브젝트 간의 충돌체로 부딪힘과 반발력을 처리
충돌체는 충돌상황에 있을 경우 유니티 충돌 메시지를 받아 상황을 확인</p>
<p>Collider 컴포넌트의 'IsTrigger'가 선택해제 되어있어야 합니다.</p>
<p>자신과 충돌 대상 모두에 Rigidbody 컴포넌트가 추가되어 있어야 하고,</p>
<p>두 Rigidbody중 하나는 IsKinematic이 체크 해제되어 있어야 합니다.</p>
<p>활성화 된 오브젝트 간의 충돌처리에 사용합니다.</p>
<p>충돌처리는 충돌지점 진입(Enter), 유지(Stay), 탈출(Exit)에 대한 함수를 지원합니다.</p>
<pre><code>private void OnCollisionEnter(Collision collision)
{
    // Enter :  충동 진입시 호출. 실행될 때 1회 실행됩니다.
}
private void OnCollisionStay(Collision collision)
{
    // Stay : 충돌중 호출. 충돌이 유지되는 동안 반복적으로 실행됩니다
}
private void OnCollisionExit(Collision collision)
{
    // Exit : 충돌 해제시 호출. 충돌이 종료될 때(벗어나는 순간) 1회 실행됩니다.
}</code></pre><h2 id="tirgger">Tirgger</h2>
<p>하나의 충돌체가 충돌을 일으키지 않고 다른 충돌체의 공간에 들어가는 것을 감지
트리거는 겹침상황에 있을 경우 유니티 트리거 메세지를 받아 상황을 확인</p>
<p>Collider 컴포넌트의 'IsTrigger'가 선택되어 있어야 합니다.</p>
<p>IsTrigger 선택시 해당 오브젝트는 물리적인 충돌이 진행되지 않고 통과됩니다.</p>
<p>자신이나 충돌 대상중 하나에 Rigidbody 컴포넌트가 추가되어 있어야 합니다.</p>
<p>주로 특정 장소 도달 등의 상황에 사용됩니다.</p>
<p>충돌처리는 충돌지점 진입(Enter), 유지(Stay), 탈출(Exit)에 대한 함수를 지원합니다.</p>
<pre><code>private void OnTirggerEnter(Collision collision)
{
    // Enter :  충동 진입시 호출. 실행될 때 1회 실행됩니다.
}
private void OnTirggerStay(Collision collision)
{
    // Stay : 충돌중 호출. 충돌이 유지되는 동안 반복적으로 실행됩니다
}
private void OnTirggerExit(Collision collision)
{
    // Exit : 충돌 해제시 호출. 충돌이 종료될 때(벗어나는 순간) 1회 실행됩니다.
}</code></pre><h2 id="layer">Layer</h2>
<p>레이어기반 충돌 &amp; 트리거 감지</p>
<ul>
<li><p>게임오브젝트의 레이어를 활용하여 충돌체간의 충돌가능 여부를 설정 가능</p>
</li>
<li><p>충돌 여부를 제외한 레이어간의 충돌은 무시됨</p>
</li>
<li><p>edit -&gt; ProjectSettings -&gt; Physics -&gt; Layer Collision Matrix</p>
</li>
</ul>
<pre><code>    /**********************************************************************************
     * 충돌체 &amp; 트리거 종류
     * 
     * 두 게임오브젝트가 충돌하면 리지드바디의 환경설정에 따라 다른 반응을 할 수 있음
     * 일부 조합의 경우 두 게임오브젝트 중에서 하나만 충돌의 영향을 받음
     * 일반적으로 Rigidbody 컴포넌트가 있는 게임오브젝트가 물리가 적용되는 것이 원칙
     **********************************************************************************/

     &lt;충돌체 종류&gt;
     (1) 정적 충돌체 (Static Collider)
     Rigidbody가 없는 충돌체, 외부에 힘에 움직이지 않음
     절대로 움직이지 않는 지형, 구성요소에 주로 사용

     (2) 리지드바디 충돌체 (Rigidbody Collider)
     Rigidbody가 있는 충돌체, 외부에 힘을 받아 움직임
     충돌하여 힘을 받아 움직이는 물체에 사용

     (3) 키네마틱 충돌체 (Kinematic Collider)
     Kinematic Rigidbody가 있는 충돌체, 외부의 힘에 반응하지 않음
     움직이지만 외부 충격에는 밀리지 않는 물체에 사용
     Kinematic 상태를 활성화/비활성화 하여 움직임 여부를 설정하는 경우에도 사용


     &lt;충돌체 &amp; 트리거 상호작용 매트릭스&gt;
     충돌체와 트리거의 종류에 따라 메시지가 전송되는 경우가 다름
     편의상 정적충돌체(SC), 리지드바디충돌체(RC), 키네마틱충돌체(KC)로 표현
     편의상 정적트리거(ST), 리지드바디트리거(RT), 키네마틱트리거(KT)로 표현

     충돌시 충돌 메시지가 전송
          SC  RC  KC  ST  RT  KT
     SC        O
     RC    O   O   O
     KC        O
     ST
     RT
     KT

     트리거시 트리거 메시지가 전송
          SC  RC  KC  ST  RT  KT
     SC                    O   O
     RC                O   O   O
     KC                O   O   O
     ST        O   O       O   O
     RT    O   O   O   O   O   O
     KT    O   O   O   O   O   O</code></pre>