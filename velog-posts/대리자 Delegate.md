<h1 id="delegate-대리자">Delegate 대리자</h1>
<p>특정 매개 변수 목록 및 반환 형식이 있는 함수에 대한 참조
대리자 인스턴스를 통해 함수를 호출 할 수 있음</p>
<h3 id="델리게이트-정의">델리게이트 정의</h3>
<p>Delegate 반환형 델리게이트이름(매개변수들);</p>
<h3 id="델리게이트-사용">델리게이트 사용</h3>
<p>반환형과 매개변수가 일치하는 함수를 델리게이트 변수에 할당
델리게이트 변수에 참조한 함수를 대리자를 통해 호출 가능</p>
<p>Invoke : 보관한 함수 부르는 기능</p>
<h1 id="콜백함수">콜백함수</h1>
<p>델리게이트를 이용하여 특정조건에서 반응하는 함수를 구현 = 알람기능
함수의 호출(Call)이 아닌 역으로 호출받을 때 반응을 참조하여 역호출</p>
<pre><code>
namespace Delegate
{
    class Callback
    {                    
            public class File
            {
                public void Save()
                {
                    Console.WriteLine(&quot;저장합니다.&quot;);
                }

                public void Load()
                {
                    Console.WriteLine(&quot;불러옵니다.&quot;);
                }
            }

            public class Button
            {
                // 버튼의 타입 별로 모두 만들어서 switch 구문을 사용하는 것도 말이 안된다.
                enum Type { }


                public delegate void ClickListener();
                public ClickListener clicklistener;

                public virtual void Click()
                {
                    if (clicklistener != null)
                    {
                        clicklistener();
                    }
                }
            }
            // 게임 속 존재하는 모든 버튼을 일일이 다 클래스로 만들 수 없다.
            public class SaveButton : Button
            {
                public override void Click()
                {

                }
            }
            static void Main(string[] args)
            {
                File file = new File();

                Button saveButton = new Button();
                saveButton.clicklistener = file.Save;
                Button loadButton = new Button();
                loadButton.clicklistener = file.Load;

                saveButton.Click(); // 저장하기
                loadButton.Click(); // 불러오기

                Player player = new Player();
                Button jumpButton = new Button();
                jumpButton.clicklistener = player.Jump;

                jumpButton.Click(); // 플레이어 점프하기
            }

            public class Player
            {
                public void Jump()
                {
                    Console.WriteLine(&quot;플레이어가 점프합니다.&quot;);
                }
            }
        }
    }
</code></pre><h1 id="일반화-델리게이트">일반화 델리게이트</h1>
<p>개발과정에서 많이 사용되는 델리게이트의 경우 일반화된 델리게이트를 사용</p>
<p>C#에서 미리 만들어놓은 델리게이트 - Action&lt;...&gt;</p>
<h1 id="func-델리게이트">Func 델리게이트</h1>
<p>반환형과 매개변수를 지정한 델리게이트
Func&lt;매개변수1, 매개변수2, ...,마지막에 반환형&gt; func;
void는 일반화 할수 없다</p>
<h1 id="action-델리게이트">Action 델리게이트</h1>
<p>반환형이 void 이며 매개변수를 지정한 델리게이트
Action&lt;매개변수1, 매개변수2, ...&gt;</p>
<h1 id="델리게이트-체인">델리게이트 체인</h1>
<p>델리게이트 변수에 여러개의 함수를 참조하는 방법</p>
<h1 id="이벤트-event">이벤트 event</h1>
<p>일련의 사건이 발생했다는 사실을 다른 객체에게 전달
델리게이트의 일부 기능을 제한하여 이벤트의 용도로 사용
델리게이트 앞에 event 키워드 붙인다
event 키워드 붙은 델리게이트는 대입 기능 제약(오히려 실수를 안하게 아기위해 막는다)
외부에서 호출을 못하게 막는다</p>
<p>델리게이트 체인과 이벤트의 차이점
델리게이트 또한 체인을 통하여 이벤트로서 구현이 가능
하지만 델리게이트는 두가지 사항 때문에 이벤트로서 사용하기 적합하지 않음</p>
<ol>
<li>= 대입연산을 통해 기존의 이벤트에 반응할 객체 상황이 초기화 될 수 있음</li>
<li>클래스 외부에서 이벤트를 발생시켜 원하지 않는 상황에서 이벤트 발생 가능
event 키워드를 추가할 경우 델리게이트에서 위 두가지 기능을 제한하여 이벤트 전용으로 사용을 유도 할 수 있다
즉, event 변수는 델리게이트에서 기능을 제한하여 이벤트 전용의 기능만으로 사용하는 기능</li>
</ol>
<p>무명메서드와 람다식
델리게이트 변수에 할당하기 위한 함수를 소스코드 구문에서 생성하여 전달
전달하기 위한 함수가 간단하고 일회성으로 사용될 경우에 간단학 작성</p>
<p>무명메서드
함수를 통한 연결은 함수가 직접적으로 선언되어 있어야 사용 가능
할당하기 위한 함수가 간단하고 자주 사용될수록 비효율적
간단한 표현식을 통해 함수를 즉시 작성하여 전달하는 방범</p>
<pre><code>Func&lt;int, int, int&gt; pow = delegate (int n, int x)
{
    int result = 1;
    for (int i = 0; i &lt; x; i++)
    {
        result *= n;
    }
    return result;
};</code></pre><p>람다식 (=&gt;)
무명메서드의 간단한 표현식</p>
<pre><code>pow = (n, x) =&gt;
{
    int result = 1;
    for (int i = 0; i &lt; x; i++)
    {
        result *= n;
    }
    return result;
};</code></pre>