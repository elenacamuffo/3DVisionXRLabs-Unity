# **Unity Lab 1: Introduction to Unity 3D and Computer Graphics**

*By Elena Camuffo, PhD Student*  
_A.Y. 2022/2023_

---

Unity 3D is a powerful cross-platform game engine and IDE used to create interactive 2D, 3D, VR, and AR applications. This post provides an overview of Unity basics, including installation, core concepts, and an introductory lab exercise.

---

### **Unity Installation**

To get started with Unity:
1. Download **Unity Hub**: [Unity Hub Download](https://unity3d.com/get-unity/download).
2. Create an account and log in.
3. Install Unity (e.g., version 2021.3.2f1) via the **Installs** tab.
4. Add platform-specific components as needed.

---

### **Unity Interface Overview**

Unity's workspace includes the following key elements:

- **Hierarchy Window**: Displays all Game Objects in the scene and their relationships.
- **Project/Console Window**: Shows project assets and debug messages.
- **Scene/Game View**: Scene editor and game preview.
- **Inspector Window**: Displays properties of the selected Game Object.
- **Toolbar**: Includes basic controls for scene manipulation and simulation.

---

### **Core Concepts**

#### **Game Objects and Assets**
- **Game Objects**: The basic building blocks in Unity scenes, such as cameras, lights, and 3D objects.
- **Assets**: Files like textures, sounds, or models imported into Unity to be used in the project.

##### **Hierarchy and Drag-and-Drop**
Game Objects can be organized hierarchically, where a parent object acts as a container for its children. Assets can be dragged and dropped directly into the scene.

#### **Cameras and Lights**
- **Cameras**: Define the scene's view.
- **Lights**: Illuminate the scene and enhance shading.

#### **Components**
Components add functionality or properties to Game Objects (e.g., physics, behavior scripts). To add a component:
- Use the **Add Component** button in the Inspector.
- Drag an asset onto a Game Object in the Scene View.

---

### **Materials and Textures**
- **Materials**: Define how an object's surface should be rendered.
- **Textures**: Bitmap images applied to materials, controlling properties like color and reflectivity.

---

### **Particle Systems**
Particle systems create effects like explosions or fire. They can be standalone Game Objects or added as components.

---

### **Scripting in Unity**
Unity supports C# and JavaScript (deprecated). Scripts control behaviors and events. Key methods include:
- `Start()`: Called at initialization.
- `Update()`: Called every frame.

#### **Example Script: Moving a Cube**
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Cube : MonoBehaviour
{
    [SerializeField]
    private float speed = 1;

    void Start()
    {
        Debug.Log("Started!");
    }

    void Update()
    {
        float deltaX = speed * Time.deltaTime;
        transform.position = new Vector3(deltaX, 0, 0) + transform.position;

        if (Mathf.Abs(transform.position.x) > 10)
            transform.position -= new Vector3(Mathf.Sign(transform.position.x) * 10, 0, 0);
    }
}
```

---

### **Augmented Reality with Vuforia**
Vuforia is a Unity-compatible SDK for AR applications. To set up:
1. Download and install Vuforia: [Vuforia SDK](https://developer.vuforia.com/downloads/sdk).
2. Add an **AR Camera** Game Object to the scene.
3. Use image-based markers to place virtual objects in the real world.

---

### **Lab Exercise: Earth System**

#### **Objective**
Create a solar system scene with AR features.

#### **Steps**
1. **Build the Scene**:
   - Add a sphere Game Object.
   - Assign a new material and texture to it.
   - Add a light and position the camera.

2. **Animate the Sphere**:
   - Create a script to rotate the sphere around its y-axis using `Transform.rotation`.

3. **Add AR Features**:
   - Integrate a Vuforia AR Camera and a marker to visualize the sphere.

4. **Advanced Features**:
   - Add the Moon and animate its orbit around the sphere.
   - Optionally, add the Sun and other planets for a complete Solar System.

---

### **Additional Resources**
- [Unity Manual](https://docs.unity3d.com/Manual/)
- [Unity Scripting API](https://docs.unity3d.com/ScriptReference)
- [Vuforia SDK](https://developer.vuforia.com/downloads/sdk)

---

Happy coding and exploring Unity 3D!