# Unity Lab 3: Animator Controller and Animations

## **Animator Controller & Animations**

*By Elena Camuffo, PhD Student*  
_A.Y. 2022/2023_

---

Unity provides robust tools for animating Game Objects using the **Animation** window and the **Animator Controller**. This lab explores creating animations, managing transitions, and scripting behaviors using these tools.

---

### **Key Concepts in Unity Animation**

#### **1. Animations**
- The Animation window allows animating Game Object properties over time.
- **Keyframes** define the values of properties at specific instants.
- Animations overwrite `Transform` positions; to maintain flexibility, animate within a parent Game Object's local coordinates.
- Nested animations can be achieved by organizing objects hierarchically.

#### **2. Creating Animations**
Steps to create an animation:
1. Press the **Record** button.
2. Move the Game Object to the desired position at key moments.
3. Add keyframes to define the animation path.
4. Use the **Curve Tab** for fine control of timing.

#### **3. Animator Controller**
- Manages animation clips and transitions using a **Finite State Machine**.
- Transitions between states are controlled by parameters (e.g., Boolean, Integer).
- Add an Animator Controller component to Game Objects for animation control.

---

### **Animation Resources**

#### **Asset Stores**
- [Unity Asset Store](https://assetstore.unity.com/)
- [Mixamo (Adobe)](https://www.mixamo.com/)
  - Use `.Fbx` format for importing characters and animations.
  - Download animations "Without Skin" for pre-existing characters.

---

### **Script Example: Animation Control**

Here’s a script to control animations using triggers:

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GrannyControls : MonoBehaviour
{
    private Animator anim;

    void Start()
    {
        anim = GetComponent<Animator>();
    }

    void Update()
    {
        if (Input.GetKeyDown("space"))
        {
            anim.SetTrigger("Jump");
        }
    }
}
```
- **Start()**: Loads the Animator Controller.
- **Update()**: Activates the `Jump` trigger when the spacebar is pressed.

---

### **Lab Exercise: Sporty Granny**

#### **Objective**
Create a dynamic environment and control animations for a character using the Animator Controller.

#### **Steps**
1. **Organize the Environment**
   - Open the `SportyGranny_Exercise` project.
   - Build the scene using prefabs from the **LowPolyEnvironment** folder.
   - Set static objects appropriately.

2. **Add the Sporty Granny**
   - Import the `SportyGranny` prefab and make it a dynamic Game Object.
   - Add animations (e.g., `Walking`) to the Animator Controller and link them to the default state.

3. **Control Animations**
   - Complete the `GrannyControl` script to trigger animations based on user input.

4. **Advanced Features**
   - Add camera follow functionality.
   - Rotate the character based on the walking direction.

5. **Optional Challenges**
   - Import the `FitnessCube` prefab and animate it to bounce based on the **Principles of Animation**.
   - Resource: [Principles of Animation Video](https://www.youtube.com/watch?v=uDqjIdI4bF4&list=WL&index=3&t=341s)

---

### **Additional Resources**
- [Unity Animation Documentation](https://docs.unity3d.com/Manual/AnimationSection.html)
- [Unity Animator Controller Documentation](https://docs.unity3d.com/Manual/AnimatorControllers.html)
- [Unity Machine Learning Agents](https://unity3d.com/how-to/unity-machine-learning-agents)

---

Happy animating with Unity!

