<h1 id="라이프-사이클">라이프 사이클</h1>
<p>유니티는 라이프 사이클을 통해 프레임에서 이뤄져야 할 동작, 즉 연산들을 수행하고 플레이어에게 그래픽으로 결과를 보여줍니다. 게임의 성능 최적화란, 적은 자원을 소모하면서도 더 큰 퍼포먼스를 보여주도록 요소를 구성하는 작업을 칭합니다.</p>
<pre><code>라이프 사이클을 알아야 코드를 쉽게 제어할 수 있습니다.
라이프 사이클을 알지 못하면 간단한 코드마저 작성하기 매우 어렵습니다.</code></pre><h1 id="유니티-함수">유니티 함수</h1>
<p>유니티 메시지 || 이벤트 함수</p>
<ul>
<li>유니티가 보내는 메시지에 반응하는 함수</li>
<li>MonoBehaviour 클래스에 메시지와 같은 이름의 함수가 반응</li>
<li>스크립트는 유니티 엔진이 보내는 메시지를 받아 사건 타이밍을 확인</li>
<li>메시지 함수에서 자신의 행동을 정의하여 기능을 구성</li>
</ul>
<h3 id="awake">Awake()</h3>
<pre><code>private void Awake()
        {           
            Debug.Log(&quot;Awake&quot;);
        }
</code></pre><ul>
<li><p>오브젝트의 '생성'시 또는 스크립트가 씬에 포함되었을 때 단 1회만 호출됩니다.</p>
</li>
<li><p>스크립트가 비활성화 되어 있는 경우에도 호출됩니다.</p>
</li>
<li><p>역할 : 스크립트가 필요로 하는 초기화 작업 진행
(외부 게임상황과 무관한 초기화 작업)</p>
</li>
</ul>
<h3 id="start">Start()</h3>
<pre><code>private void Start()
        {
            Debug.Log(&quot;Start&quot;);
        }</code></pre><ul>
<li><p>Awake() 이후 오브젝트의 '생성 및 활성화'시 단 1회만 호출됩니다.</p>
</li>
<li><p>스크립트가 씬에 처음으로 Update하기 직전에 1회 호출됩니다.</p>
</li>
<li><p>스크립트가 비활성화 되어 있는 경우 호출되지 않습니다.</p>
</li>
<li><p>역할 : 스크립트가 필요로 하는 초기화 작업 진행
(외부 게임상황이 필요한 초기화 작업)</p>
</li>
</ul>
<h3 id="onenable">OnEnable()</h3>
<pre><code>private void OnEnable()
        {
            Debug.Log(&quot;OnEnable&quot;);
        }</code></pre><ul>
<li><p>오브젝트의 '활성화'시마다 1회 호출되며, Update() 이전에 호출됩니다.</p>
</li>
<li><p>스크립트가 활성화될 때마다 호출</p>
</li>
<li><p>역할 : 스크립트가 활성화 되었을 때 작업 진행</p>
</li>
</ul>
<h3 id="update">Update()</h3>
<pre><code> private void Update()
        {
            Debug.Log(&quot;Udpate&quot;);
        }</code></pre><ul>
<li><p>매 프레임마다 1회 호출되며, 오브젝트와 스크립트의 생존 및 활성화 시에만 동작합니다.</p>
</li>
<li><p>역할 : 핵심 게임 로직 구현</p>
</li>
</ul>
<h3 id="lateupdate">LateUpdate()</h3>
<pre><code>private void LateUpdate()
        {
            Debug.Log(&quot;LateUpdate&quot;);
        }</code></pre><ul>
<li><p>게임의 프레임 마지막마다 호출</p>
</li>
<li><p>씬의 모든 게임오브젝트의 Update가 진행된 후 호출</p>
</li>
<li><p>역할 : 게임프레임의 진행 결과가 필요한 동작이 있는 기능 구현</p>
</li>
</ul>
<h3 id="fixedupdate">FixedUpdate()</h3>
<pre><code> private void FixedUpdate()
        {
            Debug.Log(&quot;FixedUdpate&quot;);
        }</code></pre><ul>
<li><p>일정한 시간(기본 1초에 50번) 마다 호출한다.</p>
</li>
<li><p>Update와 다르게 프레임당 연산과 단위시간이 일정</p>
</li>
<li><p>물리엔진과 같이 게임의 프레임과 무관하게 일정해야 하는 작업에 사용한다.</p>
</li>
<li><p>게임로직 등 연산이 많은 작업을 FixedUpdate에 구현하지 않는다.</p>
</li>
<li><p>역할 : 물리엔진 작업 진행</p>
</li>
</ul>
<h3 id="ondisable">OnDisable()</h3>
<pre><code>private void OnDisable()
        {
            Debug.Log(&quot;OnDisable&quot;);
        }</code></pre><ul>
<li><p>스크립트 또는 오브젝트의 '비활성화'시마다 1회 호출되며, Update() 이후에 호출됩니다.</p>
</li>
<li><p>역할 : 스크립트가 비활성화 되었을 때 작업 진행</p>
</li>
</ul>
<h3 id="ondestroy">OnDestroy()</h3>
<pre><code> private void OnDestroy()
        {
            Debug.Log(&quot;OnDestroy&quot;);
        }</code></pre><ul>
<li><p>스크립트가 씬에서 삭제되었을 때 또는 오브젝트의 '파괴' 시 1회 호출됩니다.</p>
</li>
<li><p>역할 : 스크립트가 필요로 하는 마무리 작업 진행</p>
</li>
</ul>
<p>Coroutine
연산 수행시 Update() 이후에 수행하지만 실행과 정지를 사용자가 자유롭게 사용할 수 있는 서브루틴입니다.</p>