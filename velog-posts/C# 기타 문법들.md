<p>Named Parameter
함수의 매개변수 순서와 무관하게 이름을 통해 호출</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/0710d777-49ba-4c62-917d-9c8274e75d46/image.png" /></p>
<p>Optional Parameter
함수의 매개변수가 초기값을 갖고 있다면, 함수 호출시 생략하는 것을 허용하는 방법</p>
<p>초기값이 있는 매개변수는 뒤부터 배치</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/efee3f4d-6d4d-410f-8db9-04c7aee69dd0/image.png" /></p>
<p>Params Parameter
매개변수의 갯수가 정해지지 않은 경우, 매개변수의 갯수를 유동적으로 사용하는 방법</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/2ee22188-1eda-4dda-926c-888c70fab6bb/image.png" /></p>
<p>Out Parameter
매개변수를 출력전용으로 설정
함수의 반환값 외에 추가적인 출력이 필요한 경우 사용</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/a425988f-7d65-45fc-a975-8653b9926f20/image.png" /></p>
<p>in Parameter
매개변수를 입력전용으로 설정
함수의 처음부터 끝까지 동일한 값을 보장하게 된다</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/99961df8-c40f-4abd-b88b-21b8a562fe6f/image.png" /></p>
<p>ref Parameter
매개변수를 원본참조로 전달
매개변수가 값형식인 경우에도 함수를 통해 원본값을 변경하고 싶을 경우 사용</p>
<p>Property</p>
<p>읽고 쓰는 권한을 따로따로 주는 역활
Get &amp; Set 함수의 간소화 표현</p>
<pre><code>public int MP{ get; , set; }</code></pre><p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/121fbb58-f4e2-4412-9fe7-42c9e11d19c8/image.png" /></p>
<p>Getter Setter</p>
<p>맴버변수가 외부객체와 상호작용하는 경우 Get &amp; Set 함수를 구현해 주는 것이 일반적
Get &amp; Set 함수의 접근제한자를 설정하여 외부에서 맴버면수의 접근을 캡슐화함
Get &amp; Set 함수를 거쳐 맴버변수에 접근할 경우 호출스택에 함수가 추가되어 변경시점을 확인 가능</p>
<p>Partial Type
클래스, 구조체, 인터페이스를 분할하여 구현하는 방범
대규모 프로젝트에서 작업하는 경우 분산하여 구현에 유용</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/f19193a7-1bb3-4688-b5a9-c84214e47b39/image.png" /></p>
<p>Nullable
Null 조건연산자
?앞의 객체가 null 인 경우 null 반환
?앞의 객체가 null 이 아닌경우 접근</p>
<p><img alt="" src="https://velog.velcdn.com/images/zxc0cc/post/33b1da6f-00bd-400f-a1ab-f69329e22d6d/image.png" /></p>