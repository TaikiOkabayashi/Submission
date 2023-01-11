///
/// 弱点をランダムに生成するスクリプト
///
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Jakuten : MonoBehaviour
{
    [SerializeField] List<GameObject> _jakutens = new List<GameObject>();
    GameObject cube = default;
    
    public void JakutenCreate()
    {
        int rnd = Random.Range(0, 3);
        Vector3 position = _jakutens[rnd].transform.position;
        cube = GameObject.CreatePrimitive(PrimitiveType.Cube);
        cube.transform.position = position;
        Invoke("Destroy", 1);
    }
    private void Destroy()
    {
        Destroy(cube);
    }
}
///
///　DOTweenを使って任意の数字にTextを徐々に変更させるスクリプト
///
using DG.Tweening;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class EnemyHpTextAnimation : MonoBehaviour
{
    [SerializeField] private Text Text= default;
    [SerializeField] private int _Hp;

    private void Start()
    {
        Text.DOCounter(0, _Hp, 1f)
        .SetEase(Ease.InOutCubic)
        //.SetLink(gameObject)
        .Play();
    }
}
///
///シリンダーを０から１００にするスクリプト
///
using DG.Tweening;
using UnityEngine;
using UnityEngine.UI;


public class EnemyHpGaugeAnimation : MonoBehaviour
{
    public void SetSliderValue(Slider slider,float endValue,float duration)
    {
        slider.DOValue(endValue, duration)
                     .SetEase(Ease.InOutQuad)
                     .WaitForCompletion();
    }
}
///
///DOTWeenを使ったアニメーションのスクリプト
///
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using DG.Tweening;

public class WeakPointAnimation : MonoBehaviour
{
    [SerializeField] int _weakPointTurn;
    // Start is called before the first frame update
    void Start()
    {
        var sequence = DOTween.Sequence();

        sequence.Append(transform.DOScale(new Vector3(0.15f, 0.15f, 0.15f), 1f))
                .Join(transform.DOLocalRotate(new Vector3(0, 0, 180f), 1f))
                .Append(transform.DOScale(new Vector3(0.1f, 0.1f, 0.1f), 1f))
                .Join(transform.DOLocalRotate(new Vector3(0, 0, 0f), 1f))
                .OnComplete(() => Destroy(gameObject))
                .SetLoops(_weakPointTurn);
    }
}
/////
