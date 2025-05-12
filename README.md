# State Machine для Unity | Универсальная машина состояний

## Описание
**StateMachine<T, S>** - универсальная реализация паттерна "Машина состояний" для Unity, где:
- `T` - MonoBehaviour-контекст (например, Player, Enemy)
- `S` - базовый класс состояний

## Основные возможности
| Функция         | Описание                          |
|-----------------|-----------------------------------|
| AddState()      | Регистрация нового состояния      |
| SwitchState<T>()| Безопасное переключение состояний |
| Activate()      | Вызов активации текущего состояния|
| StatesCount     | Количество состояний              |

## Как использовать
### 1. Создаем контекст
```csharp
public class Player : MonoBehaviour 
{
    private StateMachine<Player, PlayerState> _stateMachine;
    
    private void Awake() {
        _stateMachine = new StateMachine<Player, PlayerState>(this);
    }
}
```

### 2. Создаем состояния
```csharp
public class IdleState : PlayerState
{
    public override void OnEnter() {
        Debug.Log("Вошел в режим ожидания");
    }
}
```

### 3. Настраиваем State Machine
```csharp
_stateMachine.AddState(new IdleState());
_stateMachine.AddState(new RunState());

_stateMachine.SetInitialState<IdleState>();
```

## Документация API
### Класс StateMachine<T, S>
```
public void AddState(S state)  // Добавление состояние
public void SwitchState<T>()   // Переключение состояние 
public void Activate()         // Активация текущего состояния
```

### Абстрактный класс State<T>
```
public virtual void OnEnter()    // Обработчик события входа в состояние
public virtual void OnExit()     // Обработчик события выхода из состояния
public virtual void OnActivated() // Обработчик события активации состояния
```

## Пример реализации
Пример реализации данной машины состояний можно найти [в моём репозитории](https://github.com/echorenardo/LightWeightComboSystem), где она используется для управления состояниями комбо-атаки персонажа.

## Требования
- Unity 2019.4+
- .NET 4.x+
