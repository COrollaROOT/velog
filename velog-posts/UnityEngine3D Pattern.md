<p>프로그램 제작에 있어서 기존의 코드를 재사용하거나 수정해야 하는 경우가 발생할 수 있습니다.</p>
<p>하지만 대상이 되는 코드의 길이가 너무 길거나 작성한지 오래되어 레거시 코드(옛날 코드)가 되어버린 경우,</p>
<p>코드의 의도를 알아보기 힘들고 섣불리 수정할 수 없는 경우 혹은 팀 작업시 다른 팀원의 코드를 변경하지 않으면서 또는 기존의 코드를 수정하지 않으면서 객체지향의 다형성을 응용해야 하는 경우도 있을 수 있습니다.</p>
<h1 id="adapter-pattern">Adapter Pattern</h1>
<p>상이한 두 인터페이스를 호환할수 있도록 중간다리 역활을 하는 것</p>
<p>기존에 있던 코드를 변화 없이 호환 될수 있게 할수 있다</p>
<ul>
<li><p>장점</p>
</li>
<li><ul>
<li>기존 코드를 수정하지 않기 때문에 해당 코드가 변경 불가능하거나 업데이트 될 때에도 대응할 수 있다.</li>
</ul>
</li>
<li><ul>
<li>최소한의 변경으로 기존 코드를 재사용 할 수 있다</li>
</ul>
</li>
<li><p>단점</p>
</li>
<li><ul>
<li>약간의 성능 저하가 발생한다 (물론, 이슈가 되지 않을 만큼 미비한 성능 저하이다)</li>
</ul>
</li>
<li><ul>
<li>어뎁터 종류가 많아 지면 관리 하기 힘들어 질수 있다</li>
</ul>
</li>
</ul>
<p>기존 코드가 변경 불가능하거나, 업데이트를 통해 기존 코드의 내용 변경이 우려될 때 또는 레거시 코드(옛날 코드)임에도 해당 코드를 사용하는것이 효율적일 때 사용 하면 좋다.</p>
<h3 id="예시-코드">예시 코드</h3>
<h4 id="monstermanagercs">MonsterManager.cs</h4>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MonsterManager : MonoBehaviour
{
   [SerializeField] private Zombie _zombie;
   [SerializeField] private Alien _alien;

   private List&lt;IMonster&gt; _monsters = new List&lt;IMonster&gt;();

   public void Start()
   {
       _monsters.Add(new ZombieAdapter(_zombie));
       _monsters.Add(new AlienAdapter(_alien));

       foreach (var mon in _monsters)
       {
           mon.Attack();
       }
   }
}</code></pre><h4 id="zombiecs">Zombie.cs</h4>
<pre><code>public class Zombie : MonoBehaviour
{
   public void Bite()
   {
       Debug.Log(&quot;Zombie bite!&quot;);
   }
}</code></pre><h4 id="aliencs">Alien.cs</h4>
<pre><code>public class Alien : MonoBehaviour
{
   public void Shoot()
   {
       Debug.Log(&quot;Alien shoot!&quot;);
   }
}</code></pre><h4 id="adapterpatterncs">AdapterPattern.cs</h4>
<pre><code>public interface IMonster
{
   public void Attack();
}

public abstract class Adapter&lt;T&gt; : IMonster
{
   protected T Adaptee;

   public Adapter(T t)
   {
       Adaptee = t;
   }

   public abstract void Attack();
}

public class ZombieAdapter : Adapter&lt;Zombie&gt;
{
   public ZombieAdapter(Zombie z) : base(z)
   {
   }

   public override void Attack()
   {
       Adaptee.Bite();
   }
}

public class AlienAdapter : Adapter&lt;Alien&gt;
{
   public AlienAdapter(Alien a) : base(a)
   {
   }

   public override void Attack()
   {
       Adaptee.Shoot();
   }
}</code></pre><h1 id="singleton-pattern">Singleton Pattern</h1>
<p>싱글톤 패턴은 안 쓸수가 없을정도로 필수적인 디자인 패턴입니다.</p>
<p>하지만 유용하고 편리하면서도 단점이 많은 아이러니한 패턴입니다.</p>
<p>오직 한개 단일의 인스턴스만을 갖도록 보장 하며</p>
<p>전역적인 접근을 제공 합니다</p>
<p>이러한 특성은 장점과 동시에 단점으로 작용할 수 있기 때문에 정확한 정보와 구현 방법을 알고 사용하는것이 중요합니다.</p>
<pre><code>&lt;쉽게 사용할 수 있는 만큼 오용 되기 쉬운 패턴 입니다. 사용에 주의하세요&gt;

namespace DesignPattern
{
    public class Singleton
    {
        private static Singleton instance;

        public static Singleton GetInstance()
        {
            if (instance == null)
            {
                instance = new Singleton();
            }

            return instance;
        }

        private Singleton() { }
    }
}</code></pre><ul>
<li><p>구현</p>
</li>
<li><ul>
<li>단일 인스턴스를 유지하기 위해 생성자의 접근권한을 외부에서 생성할 수 없도록 제한</li>
</ul>
</li>
<li><ul>
<li>단일 인스턴스를 보관할 정적 변수를 구성</li>
</ul>
</li>
<li><ul>
<li>외부에서 접근이 가능한 GetInstance 함수를 구성</li>
</ul>
</li>
<li><ul>
<li>GetInstance 함수에서 단일 인스턴스가 없을 경우 인스턴스를 생성하여 정적 변수에 참조</li>
</ul>
</li>
<li><ul>
<li>GetInstance 함수에서 단일 인스턴스가 있을 경우 정적 변수에 참조된 인스턴스를 반환</li>
</ul>
</li>
<li><p>장점</p>
</li>
<li><ul>
<li>단일의 인스턴스 즉 하나뿐인 존재로 주요 클래스 관리자 역활에 적합 합니다.</li>
</ul>
</li>
<li><ul>
<li>전역적인 접근을 보장하기 때문에 싱글톤을 사용해 오브젝트들이 서로를 참조하고 있는 결합도를 낮춰 빠르게 접근 할수 있습니다.</li>
</ul>
</li>
</ul>
<ul>
<li><ul>
<li>게임 내에서 파괴되지 않기 때문에 보다 편하게 데이터를 보관할 수 있습니다.</li>
</ul>
</li>
<li><ul>
<li>인스턴스들이 싱글톤을 통하여 데이터 공유하기 쉽다.</li>
</ul>
</li>
<li><p>단점</p>
</li>
<li><ul>
<li>전역적인 접근이 가능하기 때문에 데이터에 대한 보호수준을 주의하지 않으면, 코드 결합도가 높아져 의도치 않은 데이터 변화가 발생할 수 있습니다.</li>
</ul>
</li>
<li><ul>
<li>객체들이 너무 많은 책임을 싱글톤 객체의 데이터에 의존하게 되어 단일책임원칙을 위반한는 현상이 발생할 수 있습니다.</li>
</ul>
</li>
<li><ul>
<li>static을 사용해 정적 메모리에 할당되므로, 싱글톤 객체가 많을수록 가용 메모리가 적어집니다. 또한 단위 테스트를 하기 어렵습니다.</li>
</ul>
</li>
</ul>
<h1 id="observer-pattern">Observer Pattern</h1>
<p>옵저버 패턴은 주시 대상(Subject)이 되는 객체가 자신의 데이터 변경 시 등록된 관찰자(Observer)들에게 알려주는 디자인 패턴입니다.</p>
<p>이를 통해 주기적으로 확인하지 않아도 데이터 변화에 대응할 수 있으므로 게임 최적화의 의도와 잘 부합하는 패턴이라 말할 수 있습니다.</p>
<ul>
<li><p>Subject
주시대상이 되는 데이터와 옵저버들을 가지고 있는 주체입니다. 데이터 변경시 등록된 여러 옵저버들에게 메서드를 통해 메시지를 전달합니다.</p>
</li>
<li><p>Observer
Subject를 주시하고 있는 관찰자이며, 데이터 변경에 대한 메시지 수신 시 자신이 해야 할 동작을 수행합니다.</p>
</li>
</ul>
<h2 id="옵저버-패턴-사용시의-주의점">옵저버 패턴 사용시의 주의점</h2>
<p>옵저버 패턴은 객체간의 결합도를 낮추고 불필요한 연산을 최소화 한다는 점에서 객체지향적 설계와 잘 맞지만, 사용상의 주의점이 요구됩니다.</p>
<ul>
<li><p>더 이상 사용하지 않는 객체는 구독을 해지하기</p>
</li>
<li><ul>
<li>옵저버패턴은 구독자를 주체에 '등록'하는 방식입니다. 앞으로 사용하지 않을 객체에서 구독 해지를 하지 않는다면, 불필요한 메모리 공간을 차지합니다.</li>
</ul>
</li>
<li><p>옵저버가 많아질수록 무거워진다</p>
</li>
<li><ul>
<li>성능적으로 이득을 보는 것은 사실이지만, 구독자의 수가 늘어날수록 구독자 목록을 순회하며 호출 함수를 실행하기 때문에 구독자의 수와 성능이 반비례합니다.</li>
</ul>
</li>
<li><p>구조 복잡도 증가</p>
</li>
<li><ul>
<li>옵저버 패턴은 객체 간의 결합력이 낮아지는 이점이 있지만 객체간의 관계가 불명확할 수 있습니다. 간결하고 명확한 코드를 작성해야 하며, 이는 설계 단계에서 중요하게 생각해야 할 문제입니다.</li>
</ul>
</li>
</ul>