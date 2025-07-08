<p>Game Manager를 작업 중 모든 Manager가</p>
<p>싱글톤 기반으로 작성 되는것을 기반으로 작성 중</p>
<p>모든 매니저에 일일히 싱글톤 기반 코드를 작성</p>
<pre><code>private static T instance;

    public static T Instance
    {
        get
        {
            if (!instance)
            {
                var assets = Resources.LoadAll&lt;T&gt;(&quot;&quot;);
                if (assets.Length &gt; 0)
                    instance = assets[0];
                else
                    Debug.LogError($&quot;[{typeof(T)}] Singleton 인스턴스를 찾을 수 없습니다.&quot;);
            }
            return instance;</code></pre><p>이렇게 모든 매니저 스트립트에 싱글톤 생성 인스턴스를 계속 쓰고 있었는데</p>
<p>이렇게하니 모든 싱글톤 기반</p>
<p>매니저 스크립트 코드의 가독성과 가시성이</p>
<p>굉장히 안좋고 비욜율적으로 돌아가는것을 발견</p>
<p>이것을 통합하는 싱글톤 스크립트를 작성하고</p>
<p>모든 매니저 스크립트가 싱글톤을 상속 받아갈수 있게</p>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

// 추상화 및 커스텀 Init 확장성을 위해
public abstract class Singleton&lt;T&gt; : MonoBehaviour where T : MonoBehaviour
{
    private static T instance;
    public static T Instance
    {
        get
        {
            if (instance == null)
            {
                instance = FindObjectOfType&lt;T&gt;();
                if (instance != null) return instance;

                GameObject go = new GameObject(typeof(T).Name); // 이름 동적 생성!
                instance = go.AddComponent&lt;T&gt;();
                DontDestroyOnLoad(go);
            }
            return instance;
        }
    }

    protected virtual void Awake()
    {
        if (instance == null)
        {
            instance = this as T;
            DontDestroyOnLoad(gameObject);
            OnAwake(); // 커스텀 확장 지점
        }
        else if (instance != this)
        {
            Destroy(gameObject);
        }
    }

    // 자식에서 커스텀 Awake
    protected virtual void OnAwake() { }

    // 매니저 일괄 Init을 위한 추상화 (Manager에서 직접 호출 가능)
    public virtual void Init() { }

    private void OnApplicationQuit()
    {
        instance = null;
    }

    public void DestroyManager()
    {
        if (instance != null)
        {
            Destroy(gameObject);
        }
    }
}

</code></pre><p>Singleton 스크립트를 작성</p>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;


{


    public class SOSingleton&lt;T&gt; : ScriptableObject where T : ScriptableObject
    {
        private static T instance;
        public static T Instance
        {
            get
            {
                if (instance == null)
                    instance = Resources.Load&lt;T&gt;(typeof(T).Name); // 파일명/리소스명 일치
                return instance;
            }
        }

        public virtual void Init() { }
    }
}
</code></pre><p>또한 스크립터블 오브젝트도 상속 받을수 있게 따로 작성</p>
<p>코드의 접근성을 넓혀 봤습니다</p>
<p>이렇게 코드를 따로 작성해 놓으면 각 매니저들은 </p>
<pre><code>public class GameManager : Singleton&lt;GameManager&gt;

public class AudioManagerSO : SOSingleton&lt;AudioManagerSO&gt;

public override void Init()
{
    // 후에 필요시
}</code></pre><p>그저 클래스명만 변경해주면 따로 코드 작성할 필요없이</p>
<p>작성되있는 싱글톤을 상속받아 쓸수있게 됩니다</p>
<p>필요시 Init()을 따로 쓸수 있습니다</p>
<hr />
<p>개발중인 게임 특성상 게임시작시에 먼저 불러와야하는</p>
<p>Save데이터와 같이 특정 매니저의 순서를 정해줄 필요가 있어</p>
<p>매니저 클래스를 따로 작성하고 </p>
<p>모든 매니저들의 Init 순서 결정하는걸로</p>
<p>코드를 구현했습니다</p>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.TextCore.Text;


    public static class Manager
    {
        public static SaveManager Save =&gt; SaveManager.Instance;
        public static GameManager Game =&gt; GameManager.Instance;
        public static InputManager Input =&gt; InputManager.Instance;
        public static GameSceneManager GameScene =&gt; GameSceneManager.Instance;

        public static StageManager Stage =&gt; StageManager.Instance;
        public static CharacterManager Character =&gt; CharacterManager.Instance;
        public static EnemyManager Enemy =&gt; EnemyManager.Instance;
        public static UIManager UI =&gt; UIManager.Instance;
        public static ScoreManager Score =&gt; ScoreManager.Instance;
        public static DialogueManager Dialogue =&gt; DialogueManager.Instance;

        public static AudioManagerSO Audio =&gt; AudioManagerSO.Instance;

        public static SceneChangerManagerSO SceneChanger =&gt; SceneChangerManagerSO.Instance;


        /*void Awake()
        {
            //SaveManager.Instance.Init();
            //GameManager.Instance.Init();
            //CharacterManager.Instance.Init();
            //EnemyManager.Instance.Init();
            //UIManager.Instance.Init();
           //AudioManager.Instance.Init();
            //DialogueManager.Instance.Init();
        }*/

        public static void InitAll()
        {
            Audio.Init();
            SceneChanger.Init();

            Save.Init();
            Game.Init();
            Input.Init();
            GameScene.Init();
            Character.Init();
            Enemy.Init();
            UI.Init();
            Score.Init();
            Dialogue.Init();


        }
    }</code></pre><p>이로써 Manager.cs로 각 Manager들의 순서를 지정하고</p>
<p>SOSingleton/Singleton.cs 를 작성하여 Singleton을 상속 받게하여</p>
<p>코드의 활용성과 확장성을 높혔습니다</p>