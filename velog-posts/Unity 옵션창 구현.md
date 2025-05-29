<pre><code>using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using TMPro;

public class VideoSettingsManager : MonoBehaviour
{
    // 해상도 선택 Dropdown
    public ResolutionDropdown resolutionDropdown;

    // 전체화면 설정 Toggle
    public Toggle fullscreenToggle;

    // 그래픽 품질 선택 Dropdown
    public QualityDropdown qualityDropdown;

    // 지원하는 해상도 리스트
    private List&lt;Resolution&gt; resolutions = new List&lt;Resolution&gt;();

    void Start()
    {
        InitResolutions();   // 해상도 옵션 초기화
        InitFullscreen();    // 전체화면 설정 초기화
        InitQuality();       // 그래픽 품질 옵션 초기화
    }

    /// &lt;summary&gt;
    /// 해상도 옵션을 Dropdown에 추가하고 기본값 설정
    /// &lt;/summary&gt;
    void InitResolutions()
    {
        resolutions.Clear();
        resolutionDropdown.ClearOptions();

        // 현재 시스템에서 지원하는 해상도 목록 가져오기
        resolutions.AddRange(Screen.resolutions);

        List&lt;string&gt; options = new List&lt;string&gt;();
        int currentIndex = 0;

        for (int i = 0; i &lt; resolutions.Count; i++)
        {
            var res = resolutions[i];

            // 표시용 문자열 생성 (예: 1920 x 1080 @ 60.00Hz)
            string option = $&quot;{res.width} x {res.height} @ {res.refreshRateRatio.value:F2}Hz&quot;;
            options.Add(option);

            // 현재 해상도와 일치하는 인덱스를 저장
            if (res.width == Screen.currentResolution.width &amp;&amp;
                res.height == Screen.currentResolution.height &amp;&amp;
                Mathf.Approximately(res.refreshRateRatio.value, Screen.currentResolution.refreshRateRatio.value))
            {
                currentIndex = i;
            }
        }

        // Dropdown에 옵션 추가
        resolutionDropdown.AddOptions(options);

        // 이전에 저장한 인덱스 불러오기 (없으면 현재 해상도 인덱스)
        int savedIndex = PlayerPrefs.GetInt(&quot;ResolutionIndex&quot;, currentIndex);
        resolutionDropdown.value = savedIndex;
        resolutionDropdown.RefreshShownValue();

        // 선택 시 이벤트 연결
        resolutionDropdown.onValueChanged.AddListener(OnResolutionChange);

        // 초기 해상도 적용
        OnResolutionChange(savedIndex);
    }

    /// &lt;summary&gt;
    /// 전체화면 설정 초기화
    /// &lt;/summary&gt;
    void InitFullscreen()
    {
        // 저장된 값 불러오기 (없으면 현재 전체화면 상태 기준)
        bool isFullscreen = PlayerPrefs.GetInt(&quot;Fullscreen&quot;, Screen.fullScreen ? 1 : 0) == 1;
        fullscreenToggle.isOn = isFullscreen;

        // 이벤트 연결
        fullscreenToggle.onValueChanged.AddListener(OnFullscreenToggle);

        // 전체화면 설정 적용
        Screen.fullScreen = isFullscreen;
    }

    /// &lt;summary&gt;
    /// 그래픽 품질 옵션 초기화
    /// &lt;/summary&gt;
    void InitQuality()
    {
        qualityDropdown.ClearOptions();

        // Unity에서 제공하는 품질 이름 목록 가져오기
        string[] qualityNames = QualitySettings.names;
        qualityDropdown.AddOptions(new List&lt;string&gt;(qualityNames));

        // 저장된 품질 수준 불러오기 (없으면 현재 수준 사용)
        int savedLevel = PlayerPrefs.GetInt(&quot;QualityLevel&quot;, QualitySettings.GetQualityLevel());
        qualityDropdown.value = savedLevel;

        // 이벤트 연결 및 품질 적용
        qualityDropdown.onValueChanged.AddListener(OnQualityChange);
        QualitySettings.SetQualityLevel(savedLevel);
    }

    /// &lt;summary&gt;
    /// 해상도 변경 시 호출되는 메서드
    /// &lt;/summary&gt;
    void OnResolutionChange(int index)
    {
        Resolution res = resolutions[index];

        // 선택된 해상도로 변경 (전체화면 모드 유지)
        Screen.SetResolution(res.width, res.height, Screen.fullScreenMode, res.refreshRateRatio);

        // 저장
        PlayerPrefs.SetInt(&quot;ResolutionIndex&quot;, index);
    }

    /// &lt;summary&gt;
    /// 전체화면 토글 변경 시 호출
    /// &lt;/summary&gt;
    void OnFullscreenToggle(bool isFullscreen)
    {
        Screen.fullScreen = isFullscreen;

        // 저장
        PlayerPrefs.SetInt(&quot;Fullscreen&quot;, isFullscreen ? 1 : 0);
    }

    /// &lt;summary&gt;
    /// 그래픽 품질 변경 시 호출
    /// &lt;/summary&gt;
    void OnQualityChange(int index)
    {
        QualitySettings.SetQualityLevel(index);

        // 저장
        PlayerPrefs.SetInt(&quot;QualityLevel&quot;, index);
    }
}
</code></pre>