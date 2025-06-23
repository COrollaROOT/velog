<ul>
<li>필수 기능을 가진 Prototype 생성</li>
<li><ul>
<li>GameManager</li>
</ul>
</li>
<li><ul>
<li>AudioManager</li>
</ul>
</li>
<li>ScriptableObject를 사용</li>
</ul>
<h1 id="gamemanager">GameManager</h1>
<ul>
<li>Unity에서 GameManager는 게임의 전반적인 흐름과 상태를 중앙에서 관리하는 역활</li>
<li>일반적으로 Singleton 패턴을 사용하여 하나의 인스턴스만 유지하도록 설계</li>
<li>게임의 주요 시스템을 통합적으로 제어하는 기능 수행</li>
<li>게임 시작, 일시 정지,종료 등의 흐름을 제어 또는 특정 이벤트(플레이어 사망,게임 클리어)가 발생하면 적절한 동작을 수행</li>
<li>점수,플레이어 진행 상황,설정 등 데이터를 저장하고 불러오는 기능</li>
<li>JSON 파일, PlayerPrefs, ScriptableObject 등을 이용하여 데이터를 관리</li>
<li>전역적인 접근이 필요한 객체를 관리 다른 스크립트에서 쉽게 접근할 수 있도록 싱글톤 패턴을 활용</li>
<li>이벤트 시스템을 관리하여 게임에서 중요한 이벤트가 발생할 때 적절한 핸들링을 수행</li>
</ul>
<h2 id="prototype">Prototype</h2>
<h3 id="gamemanagersocs">GameManagerSO.cs</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[CreateAssetMenu(fileName = &quot;GameManager&quot;, menuName = &quot;Managers/GameManager&quot;)]
public class GameManagerSO : ScriptableObject
{
    // 게임 일시 정지 상태
    [HideInInspector] public bool isGamePaused;

    // 플레이어 점수
    [HideInInspector] public int score;

    // 점수 추가
    public void AddScore(int value)
    {
        score += value;
    }

    // 게임 일시 정지
    public void PauseGame()
    {
        isGamePaused = true;
        Time.timeScale = 0f;
    }

    // 게임 재개
    public void ResumeGame()
    {
        isGamePaused = false;
        Time.timeScale = 1f;
    }
}</code></pre><h3 id="gamemanagerrunnercs">GameManagerRunner.cs</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GameManagerRunner : MonoBehaviour
{
    public GameManagerSO gameManager;

    void Start()
    {
        // 시작 시 게임 재개 상태로 초기화
        gameManager.ResumeGame();
    }
}</code></pre><h1 id="audiomanager">AudioManager</h1>
<ul>
<li>사운드를 여러 오브젝트에 붙이고, 특정 조건이 발생하면 실행할 수 있지만
씬 규모가 커지면 관리하기 힘들수 있다</li>
<li>하나의 AudioManager를 싱글톤 패턴을 이용하여 구현 하여 다른 스크립트에서 쉽게 접근이 가능하고 관리도 용이한 형태로 AudioManager 구현</li>
<li>ScriptableObject 사용</li>
</ul>
<h2 id="prototype-1">Prototype</h2>
<h3 id="audiomanagersocs">AudioManagerSO.cs</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[CreateAssetMenu(fileName = &quot;AudioManager&quot;, menuName = &quot;Managers/AudioManager&quot;)]
public class AudioManagerSO : ScriptableObject
{
    // 런타임에서 주입받는 AudioSource들
    [HideInInspector] public AudioSource bgmSource;
    [HideInInspector] public AudioSource sfxSource;

    public void Init(AudioSource bgm, AudioSource sfx) // AudioSource를 외부에서 주입
    {
        bgmSource = bgm;
        sfxSource = sfx;
    }

    // 배경음악 재생
    public void PlayBGM(AudioClip clip)
    {
        if (bgmSource == null || clip == null) return;
        bgmSource.clip = clip;
        bgmSource.Play();
    }

    // 효과음 재생
    public void PlaySFX(AudioClip clip)
    {
        if (sfxSource == null || clip == null) return;
        sfxSource.PlayOneShot(clip);
    }

    // 배경음악 정지
    public void StopBGM()
    {
        bgmSource?.Stop();
    }
}</code></pre><h3 id="audiomanagerrunnercs">AudioManagerRunner.cs</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class AudioManagerRunner : MonoBehaviour // // AudioSource를 ScriptableObject에 연결하는 러너
{
    public AudioManagerSO audioManager;
    public AudioSource bgmSource;
    public AudioSource sfxSource;

    void Awake()
    {
        audioManager.Init(bgmSource, sfxSource); // 런타임 AudioSource 주입
    }
}</code></pre><h1 id="scenemanager">SceneManager</h1>
<ul>
<li>편집기의 플레이어와 재생 모드에서 장면을 관리 합니다</li>
<li>SceneManager를 사용하면 플레이어에서 장면을 관리하고 조작할 수 있습니다</li>
</ul>
<h2 id="prototype-2">Prototype</h2>
<h3 id="scenetransitionmanagersocs">SceneTransitionManagerSO.CS</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;


[CreateAssetMenu(fileName = &quot;SceneManager&quot;, menuName = &quot;Managers/SceneManager&quot;)]
public class SceneTransitionManagerSO : ScriptableObject
{
    // 이름으로 씬 로딩
    public void LoadScene(string name)
    {
        SceneManager.LoadScene(name);
    }

    // 현재 씬 리로드
    public void ReloadCurrentScene()
    {
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }
}</code></pre><h1 id="inputmanager">InputManager</h1>
<ul>
<li>Update() 함수 안에서 플레이어마다 키를 반복하는 방식은 매우 비효율적인 방식이다</li>
<li>공통된 기능을 이벤트로 받아 처리하는 클래스로 구현</li>
</ul>
<h2 id="prototype-3">Prototype</h2>
<h3 id="inputmanagersocs">InputManagerSO.cs</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[CreateAssetMenu(fileName = &quot;InputManager&quot;, menuName = &quot;Managers/InputManager&quot;)]
public class InputManagerSO : ScriptableObject
{
    public KeyCode pauseKey = KeyCode.Escape;

    // 일시 정지 키 입력 확인
    public bool IsPausePressed()
    {
        return Input.GetKeyDown(pauseKey);
    }
}
</code></pre><h3 id="inputmanagerrunnercs">InputManagerRunner.cs</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class InputManagerRunner : MonoBehaviour
{
    public InputManagerSO inputManager;
    public GameManagerSO gameManager;
    public UIManagerSO uiManager;

    void Update()
    {
        if (inputManager.IsPausePressed())
        {
            if (gameManager.isGamePaused)
            {
                gameManager.ResumeGame();
                uiManager.ShowPauseUI(false);
            }
            else
            {
                gameManager.PauseGame();
                uiManager.ShowPauseUI(true);
            }
        }
    }
}
</code></pre><h1 id="uimanager">UIManager</h1>
<ul>
<li>UI를 관리해주는 역활</li>
<li>전체 닫기,뒤로 가기, 예약 기능, 일시정지, 게임 재개, 설정창 적용 등</li>
</ul>
<h2 id="prototype-4">Prototype</h2>
<h3 id="uimanagersocs">UIManagerSO.cs</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[CreateAssetMenu(fileName = &quot;UIManager&quot;, menuName = &quot;Managers/UIManager&quot;)]
public class UIManagerSO : ScriptableObject
{
    [HideInInspector] public GameObject pauseUI;

    // UI 패널 객체 연결
    public void Init(GameObject pausePanel)
    {
        pauseUI = pausePanel;
    }

    // 일시 정지 UI On/Off
    public void ShowPauseUI(bool show)
    {
        if (pauseUI != null)
            pauseUI.SetActive(show);
    }
}</code></pre><h3 id="uimanagerrunnercs">UIManagerRunner.cs</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class UIManagerRunner : MonoBehaviour
{
    public UIManagerSO uiManager;
    public GameObject pausePanel;

    void Awake()
    {
        uiManager.Init(pausePanel);
    }
}
</code></pre><h1 id="objectpoolmanager">ObjectPoolManager</h1>
<ul>
<li>게임에서 객체를 생성하고 삭제하는 대신 재사용하여 성능을 최적화하는 시스템</li>
<li>미리 생성된 객체들을 풀(Pool)에 저장해두고 필요할 때마다 가져와 사용
사용후엔 다기 풀(Pool)에 반환하여 재사용(동적할당과 해제를 줄여 성능을 향상 시킬 수 있습니다)</li>
</ul>
<h2 id="prototype-5">Prototype</h2>
<h3 id="objectpoolmanagersocs">ObjectPoolManagerSO.cs</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[CreateAssetMenu(fileName = &quot;ObjectPoolManager&quot;, menuName = &quot;Managers/ObjectPoolManager&quot;)]
public class ObjectPoolManagerSO : ScriptableObject
{
    // 풀 저장소 (key: 프리팹 이름)
    private Dictionary&lt;string, Queue&lt;GameObject&gt;&gt; pool = new();

    // 오브젝트 풀 생성
    public void CreatePool(string key, GameObject prefab, int count)
    {
        if (!pool.ContainsKey(key))
            pool[key] = new Queue&lt;GameObject&gt;();

        for (int i = 0; i &lt; count; i++)
        {
            GameObject obj = Instantiate(prefab);
            obj.SetActive(false);
            pool[key].Enqueue(obj);
        }
    }

    // 풀에서 꺼내기
    public GameObject Spawn(string key, Vector3 pos, Quaternion rot)
    {
        if (!pool.ContainsKey(key) || pool[key].Count == 0) return null;

        GameObject obj = pool[key].Dequeue();
        obj.transform.SetPositionAndRotation(pos, rot);
        obj.SetActive(true);
        return obj;
    }

    // 풀에 반환
    public void Despawn(string key, GameObject obj)
    {
        obj.SetActive(false);
        pool[key].Enqueue(obj);
    }
}
</code></pre><h3 id="objectpoolrunnercs">ObjectPoolRunner.cs</h3>
<pre><code>using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ObjectPoolRunner : MonoBehaviour // 오브젝트 풀 매니저에 초기 풀 생성
{
    public ObjectPoolManagerSO poolManager;
    public GameObject prefab;
    public string key = &quot;Bullet&quot;;

    void Awake()
    {
        poolManager.CreatePool(key, prefab, 20);
    }
}
</code></pre><p>이후 필요 기술 R&amp;D</p>