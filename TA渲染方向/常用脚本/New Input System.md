# New Input System

# 获取输入

```csharp
public class GameInput : MonoBehaviour
{
    PlayerInputActions playerInputActions;
    private void Awake()
    {
        playerInputActions =  new PlayerInputActions();
        playerInputActions.Player.Enable();
    }

    public Vector2 GetMovementVectorNormalized()
    {
        Vector2 inputVector = playerInputActions.Player.Move.ReadValue<Vector2>();
        inputVector = inputVector.normalized;
        return inputVector;
    }
}
```

‍
