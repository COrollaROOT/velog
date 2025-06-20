<h1 id="싱글톤-패턴이란">싱글톤 패턴이란?</h1>
<h3 id="unity에서-싱글톤-매니저singleton-manager패턴은">Unity에서 싱글톤 매니저(Singleton Manager)패턴은</h3>
<p>게임의 전역 상태나 기능을 관리할 때 매우 유용하다</p>
<blockquote>
<p>소프트웨어 디자인 패턴에서 싱글턴 패턴(Singleton pattern)을 따르는 클래스는,
생성자가 여러 차례 호출되더라도 실제로 생성되는 객체는 하나이고 최초 생성 이후에 호출된 생성자는 최초의 생성자가 생성한 객체를 리턴한다.
이와 같은 디자인 유형을 싱글턴 패턴이라고 한다. 
주로 공통된 객체를 여러개 생성해서 사용하는 DBCP(DataBase Connection Pool)와 같은 상황에서 많이 사용된다.
출처 : <a href="https://ko.wikipedia.org/wiki/%EC%8B%B1%EA%B8%80%ED%84%B4_%ED%8C%A8%ED%84%B4">wikipedia</a></p>
</blockquote>
<ul>
<li>싱글톤 패턴은 게임구현에서 가장 많이 사용되는 디자인 패턴중 하나입니다.
단일의 인스턴스와 전역적인 접근을 제공하며 이러한 특성은 장점과 동시에 단점으로 작용할 수 있기 때문에 정확한 정보와 구현 방법을 알고 사용하는것이 중요합니다.</li>
</ul>
<p>정해져있는 관리자 객체에만 사용하도록 하자
너무 많은 책임을 주지말자
부적절한 상황에 쓰지말자
오용 하지마라</p>
<h3 id="장점">장점</h3>
<ul>
<li><p><strong><em>단일의 인스턴스</em></strong> 와 <em><strong>전역적인 접근</strong></em> 을 보장하기 때문에 싱글톤을 사용해 오브젝트들이 서로를 참조하고 있는 결합도를 낮출 수 있습니다.</p>
</li>
<li><p>게임 내에서 파괴되지 않기 때문에 보다 편하게 데이터를 보관할 수 있습니다.</p>
</li>
</ul>
<h3 id="단점">단점</h3>
<ul>
<li><p>전역적인 접근이 가능하기 때문에 데이터에 대한 보호수준을 주의하지 않으면, 의도치 않은 데이터 변화가 발생할 수 있습니다.</p>
</li>
<li><p>객체들이 싱글톤 객체의 데이터에 의존하게 되는 현상이 발생할 수 있습니다.
static을 사용해 정적 메모리에 할당되므로, 싱글톤 객체가 많을수록 가용 메모리가 적어집니다.</p>
</li>
</ul>
<p>필요 R&amp;D</p>
<h3 id="gamemanager">GameManager</h3>
<h3 id="sencemanager">SenceManager</h3>
<ul>
<li>씬 체인지 <h3 id="filemanager">FileManager</h3>
<h3 id="audiomanager">AudioManager</h3>
</li>
<li>BGM</li>
<li>SFX</li>
</ul>
<h3 id="playermanager">PlayerManager</h3>
<h3 id="anemymanager">AnemyManager</h3>
<h3 id="uimanager">UIManager</h3>
<h3 id="datamanager">DataManager</h3>
<h3 id="예시">예시</h3>
<pre><code>public class GameManager : MonoBehaviour
{
    private static GameManager instance // (GameManager static 변수로) 데이터 하나가 전역적으로 사용 되기 위해 

    public int score; // 점수

    if (instance == null) // 만약 instance가 없었으면
    {
        instance = this;    
    }
    else
    {
        Destroy(gameObject); /여러 게임 관리자 발생을 막기 위해
    }
</code></pre><pre><code>using UnityEngine;

public class Singleton&lt;T&gt; : MonoBehaviour where T : MonoBehaviour
{
    private static T instance;

    public static T Instance
    {
        get
        {
            if (instance == null)
            {
                // 씬에서 찾기
                instance = FindObjectOfType&lt;T&gt;();
                if (instance == null)
                {
                    // 없다면 새로 생성
                    GameObject singletonObj = new GameObject(typeof(T).Name);
                    instance = singletonObj.AddComponent&lt;T&gt;();
                    DontDestroyOnLoad(singletonObj);
                }
            }
            return instance;
        }
    }

    protected virtual void Awake() // 생성시 = Awake
    {
        // 중복 제거
        if (instance == null)
        {
            instance = this as T;
            DontDestroyOnLoad(gameObject);
        }
        else if (instance != this)
        {
            Destroy(gameObject);
        }
    }
}</code></pre><h3 id="gamemanager-예시">GameManager 예시</h3>
<pre><code>using UnityEngine;

public class GameManager : Singleton&lt;GameManager&gt;
{
    public int score;
    public bool isGamePaused;

    public void AddScore(int amount)
    {
        score += amount;
    }

    public void PauseGame()
    {
        isGamePaused = true;
        Time.timeScale = 0f;
    }

    public void ResumeGame()
    {
        isGamePaused = false;
        Time.timeScale = 1f;
    }

    protected override void Awake()
    {
        base.Awake(); // Singleton 초기화
        // 추가 초기화
    }
}</code></pre>