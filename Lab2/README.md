# **Unity Lab 2: Physics & User Interface (UI)**

### **Physics in Unity**

Unity offers an integrated physics engine to simulate real-world physics in your project. It ensures objects behave naturally under forces like gravity and collisions.

#### **Key Components of Unity Physics**

##### **1. Rigidbodies**
- The **Rigidbody** component enables physical behavior for Game Objects.
- With `isKinematic` enabled, a Rigidbody can be controlled through scripting without being affected by physics (e.g., gravity).

##### **2. Colliders**
- Colliders define the shape of a Game Object for collision detection.
- **Dynamic Colliders**: Require a Rigidbody and interact physically.
- **Static Colliders**: Used for immovable objects like walls and floors.

---

### **Physics Script Example**
Here’s an example of a script that changes the color of a ball upon collision with another object:

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Ball : MonoBehaviour
{
    private void OnCollisionEnter(Collision collision)
    {
        Color randomColor = SelectRandomColor();
        GetComponent<Renderer>().material.color = randomColor;
    }

    private Color SelectRandomColor()
    {
        return new Color(
            UnityEngine.Random.Range(0f, 1f),
            UnityEngine.Random.Range(0f, 1f),
            UnityEngine.Random.Range(0f, 1f)
        );
    }
}
```

---

### **Adding Player Control**

Use scripting to allow user input to control a Rigidbody:

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class AddPlayerControlledVelocity : MonoBehaviour
{
    [SerializeField] float speed = 5f;
    [SerializeField] KeyCode keyPositive;
    [SerializeField] KeyCode keyNegative;

    void FixedUpdate()
    {
        Vector3 v3Force = new Vector3((speed / 100), 0f, 0f);

        if (Input.GetKey(keyPositive))
            GetComponent<Rigidbody>().velocity += v3Force;

        if (Input.GetKey(keyNegative))
            GetComponent<Rigidbody>().velocity -= v3Force;
    }
}
```
- **FixedUpdate**: Ensures the script runs alongside the physics engine.
- Adjust the `keyPositive` and `keyNegative` variables for movement.

---

### **User Interface (UI) in Unity**

The User Interface (UI) includes visual elements such as text, buttons, and images. These components enable user interaction.

#### **Key UI Elements**
- **Canvas**: The root Game Object for drawing UI elements.
- **Text**: Displays dynamic or static text.
- **Image**: Shows a fixed or dynamic visual in the UI.

---

### **Dynamic Timer Script Example**

The following script updates a timer displayed on the Canvas:
```csharp
using UnityEngine;
using UnityEngine.UI;

public class Timer : MonoBehaviour
{
    void Start()
    {
        string currTime = "Time: 0 [s]";
        gameObject.GetComponent<Text>().text = currTime;
    }

    void Update()
    {
        string currTime = "Time: " + Mathf.Ceil(Time.time).ToString() + " [s]";
        gameObject.GetComponent<Text>().text = currTime;
    }
}
```

---

### **Lab Exercise: Ball Game**

#### **Objective**
Create a physics-based ball game with user controls and UI elements.

#### **Steps**
1. **Load the Scene**
   - Import the provided `BallGame_Exercise` base project into Unity.

2. **Add Player Control**
   - Write a script to move the ball using keyboard input.
   - Make the camera follow the ball with an offset.

3. **Add User Interface**
   - Add a "Game Over" message when the ball hits lava.
   - Add a "Victory" message when the ball reaches the target.

4. **Advanced Features**
   - Restart the game on button press using `SceneManager.LoadScene`.
   - Add levels by linking multiple scenes.

---

## **Additional Resources**
- [Unity Physics Documentation](https://docs.unity3d.com/Manual/Physics.html)
- [Unity UI Documentation](https://docs.unity3d.com/Manual/UISystem.html)

---

Enjoy building your Ball Game in Unity!