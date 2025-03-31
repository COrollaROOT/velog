<h1 id="object-형식">object 형식</h1>
<p>object 형식이란</p>
<p>C#의 존재하는 모든 클래스의 기본이 되는 자료형으로,</p>
<p>object 형식을 사용하면 데이터의 형식에 관계없이</p>
<p>object 형식의 자료형에 담을 수 있습니다.</p>
<p>참조 형식으로만 저장하여 해당 데이터를 힙에 할당하고, 주소 값만 담고 있습니다. 때문에, 데이터를 다시 활용하기 위해서는 값 형식으로 변환하는 과정이 필요</p>
<p>object C# 최상위 부모 클래스
object론 산술 연산 불가</p>
<p>업캐스팅 : 암시적으로 사용가능 
박싱 : 값형식 -&gt; 참조형식</p>
<p>다운캐스팅 : 명시적으로 해야함 
언박싱 : 참조형식 -&gt; 값형식</p>
<p>단점-느리다-안쓰는걸 최대한 권장
메모리에 부담이 간다</p>
<pre><code>static void Main(string[] args)
{

       int value = 10;

       // 업캐스팅 : 암시적으로 사용가능 // 박싱 : 값형식 -&gt; 참조형식
       object obj = value;

      // 다운캐스팅 : 명시적으로 해야함  // 언박싱 : 참조형식 -&gt; 값형식 (단점-느리다)안쓰는걸 최대한 권장
      int result = (int)obj;
}</code></pre><h1 id="제네릭--일반화">제네릭 : 일반화</h1>
<p>일반화
클래스 또는 함수가 코드에 의해 선언되고 인스턴스화될 때까지
형식의 사양을 연기하는 디자인
기능을 구현한 뒤 자료형을 사용 당시에 지정해서 사용</p>
<p>일반화 함수
일반화는 자료형의 형식을 지정하지 않고 함수를 정의
기능을 구현한 뒤 사용 당시에 자료형의 형식을 지정해서 사용</p>
<pre><code>using System.ComponentModel;

namespace Generic
{
    internal class Program
    {


        static void Main(string[] args)
        {


            int iLeft = 10;
            int iRight = 20;

            Util.Swap&lt;int&gt;(ref iLeft, ref iRight);

            float fLeft = 10.2f;
            float fRight = 20.1f;

            Util.Swap&lt;float&gt;(ref fLeft, ref fRight);

            bool bLeft = true;
            bool bRight = false;

            Util.Swap&lt;bool&gt;(ref bLeft, ref bRight);

        }
    }

    public class Util
    {

        public static void Swap&lt;T&gt;(ref T left, ref T right)
        {
            T temp = left;
            left = right;
            right = temp;
        }
    }
}
</code></pre><h2 id="일반화-자료형-제약">일반화 자료형 제약</h2>
<p>where T : ?? = T에 제시될 형식에 대한 제한사항</p>
<p>일반화 자료형을 선언할 때 제약조건을 선언하여,
사용 당시 쓸 수 있는 자료형을 제한</p>
<pre><code>    public static void Test&lt;T&gt;(T value) where T : Item
    {
        value.Use();
    }

}

public class Item
{
    public void Use() { }
}</code></pre>