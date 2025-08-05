## New Input System

<br>

[Unity's NEW input system in 13 minutes](https://www.youtube.com/watch?v=ONlMEZs9Rgw)  

<br>

오늘은 Unity에 Old Input System과 New Input Sytem의 차이점을 알아보고 간략하게 New Input System을 사용하는 방법을 알아보자

<br>

| 항목  | Old Input System | New Input System |
| --- | --- | --- |
| **기반 구조** | `Input` 클래스 기반 | 이벤트 기반 및 C# InputAction 기반 |
| **확장성** | 낮음 (플랫폼, 디바이스 확장 어려움) | 높음 (멀티 디바이스 대응, 리맵, 커스터마이징 가능) |
| **코드 스타일** | `Input.GetKey()`, `Input.GetTouch()` | `InputAction`, `PlayerInput` 등 사용 |
| **기기 대응** | 키보드, 마우스, 터치 등 제한적 | 게임패드, 모바일, VR/AR, 커스텀 디바이스 대응 |
| **입력 설정** | Unity Editor > Project Settings > Input | InputActionAsset 파일(.inputactions)로 시각적 편집 |
| **복수 입력 처리** | 멀티터치, 조이패드 등 복잡함 | 다중 디바이스 / 플레이어 인식 우수 |
| **학습 난이도** | 낮음 (빠르게 사용 가능) | 높음 (구조 파악 필요) |
| **지원 여부** | 유지보수만 진행 중 (레거시) | 공식 권장 (Unity 2021 이후 권장) |

<br>

## **Old Input System의 특징**

<br>

```
if (Input.GetMouseButtonDown(0)) {
    Debug.Log("마우스 클릭!");
}

float h = Input.GetAxis("Horizontal");
```

<br>

- `Input.GetKey()`, `Input.GetMouseButton()`, `Input.GetAxis()` 등을 통해 입력 감지
- 사용이 매우 간단하고 직관적
- **단점**: 키 리맵, 멀티디바이스, VR/AR 확장 등에 제약 많음

<br>

## <br>

## **New Input System의 특징**

<br>

```
public class PlayerController : MonoBehaviour
{
    public InputAction moveAction;
    public InputActionReference move;

    private Vector2 _moveDirection;

    private void OnEnable() => moveAction.Enable();
    private void OnDisable() => moveAction.Disable();

    void Update()
    {
        // 방법 1
        Vector2 move = moveAction.ReadValue<Vector2>();
        Debug.Log(move);

        // 방법 2 (미리 만들어둔 래퍼런스를 사용하는 방법)
        _moveDirection = move.action.ReadValue<Vector2>();
    }
}
//PlayerInput 컴포넌트 방식도 존재함
```

<br>

- Input Actions를 SO로 시각적으로 구성
    - .inputactions 파일에서 키맵핑, 액션, 디바이스, 조합 등을 구성

<br>

## ✅ 어떤 걸 써야 할까?

| 상황  | 추천 시스템 |
| --- | --- |
| 빠른 프로토타입, 간단한 입력만 필요 | **Old Input System** (빠름, 쉬움) |
| 멀티 플랫폼, 키 설정 지원, 게임패드/VR 지원 필요 | **New Input System** (확장성, 유지보수 용이) |
| Unity 2022 이상, 협업 프로젝트 | **New Input System** 권장 |

<br>

<br>