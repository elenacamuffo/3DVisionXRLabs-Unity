# Unity Lab 5: NavMesh, Raycasting, and Simulation

*By Elena Camuffo, PhD Student*  
_A.Y. 2022/2023_

---

### **Overview**

This lab focuses on Unity's capabilities for simulating environments, navigation systems, and raycasting. Key topics include NavMesh baking, simulating LiDAR sensors, and implementing advanced functionalities for navigation and mapping.

---

### **Point Cloud Types**

Point clouds can be categorized into three main types based on their acquisition methods:

1. **Static**:
   - Large point clouds representing complete 3D scenes.
2. **Sequential**:
   - Acquired incrementally with sensors like LiDAR scanners (commonly used in autonomous driving).
3. **Synthetic**:
   - Generated in simulation environments such as Unity.

---

### **Raycasting in Unity**

#### **What is Raycasting?**
- Raycasting sends a virtual ray into the scene to detect collisions with objects.
- Useful for simulating sensors, detecting object interactions, and determining visibility.

#### **Simulating LiDAR Sensors**
LiDAR sensors use raycasting to simulate light rays hitting objects in the scene. This approach is computationally efficient and provides point cloud data for the simulated environment.

#### **Raycasting Script Example**

```csharp
using UnityEngine;

public class RaycastLiDAR : MonoBehaviour
{
    [SerializeField] LayerMask layerMask;

    void FixedUpdate()
    {
        RaycastHit hit;

        if (Physics.Raycast(transform.position, transform.TransformDirection(Vector3.forward), out hit, Mathf.Infinity, layerMask))
        {
            Debug.DrawRay(transform.position, transform.TransformDirection(Vector3.forward) * hit.distance, Color.red);
            Debug.Log("Did Hit");
        }
        else
        {
            Debug.DrawRay(transform.position, transform.TransformDirection(Vector3.forward) * 100, Color.black);
            Debug.Log("Did not Hit");
        }
    }
}
```
- **Parameters**:
  - `origin`: Starting point of the ray.
  - `direction`: Direction vector for the ray.
  - `layerMask`: Filters which objects the ray interacts with.

---

### **NavMesh: Unity's Navigation System**

#### **What is NavMesh?**
- A NavMesh describes the walkable areas in a scene, enabling Game Objects to navigate intelligently.

#### **Key Components**
1. **NavMeshAgent**:
   - Represents objects that can navigate the NavMesh.
2. **NavMeshObstacle**:
   - Defines obstacles that agents avoid.
3. **Off-Mesh Links**:
   - Allow agents to navigate between disconnected areas.

#### **Baking a NavMesh**
Steps to bake a NavMesh:
1. Mark the objects in the scene as **Navigation Static**.
2. Open the **Navigation** window.
3. Adjust baking settings under the **Bake** tab.
4. Click **Bake** to generate the NavMesh.

#### **NavMesh Script Example**

```csharp
using UnityEngine;
using UnityEngine.AI;

public class MoveToClickPoint : MonoBehaviour
{
    NavMeshAgent agent;

    void Start()
    {
        agent = GetComponent<NavMeshAgent>();
    }

    void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            RaycastHit hit;
            if (Physics.Raycast(Camera.main.ScreenPointToRay(Input.mousePosition), out hit, 100))
            {
                agent.destination = hit.point;
            }
        }
    }
}
```
- **Usage**:
  - Assign the script to a NavMeshAgent Game Object.
  - Use mouse clicks to navigate the agent.

---

### **Scriptable Objects**

#### **What are Scriptable Objects?**
- ScriptableObjects store large datasets independent of GameObject instances.
- Useful for reusing data, such as spawn points or object properties.

#### **Scriptable Object Example**

```csharp
using UnityEngine;

[CreateAssetMenu(fileName = "Data", menuName = "ScriptableObjects/SpawnManagerScriptableObject", order = 1)]
public class SpawnManagerScriptableObject : ScriptableObject
{
    public string prefabName;
    public int numberOfPrefabsToCreate;
    public Vector3[] spawnPoints;
}
```

---

### **Lab Exercise: LiDAR System**

#### **Objective**
Simulate a LiDAR system using Unity's raycasting and NavMesh capabilities.

#### **Steps**
1. **Bake the NavMesh**:
   - Use the NavMesh baking tool to define walkable surfaces.
   - Assign `NavMeshAgent` to the player and `NavMeshObstacle` to other objects.

2. **Category Detection**:
   - Change the ray color based on the category of the hit object.
   - Use Scriptable Objects or LayerMasks to categorize objects.

3. **LiDAR Point Cloud Simulation**:
   - Increase the number of rays in the raycaster.
   - Rotate the raycaster to simulate a 360° LiDAR scan.
   - Store acquired points in `.txt` files with their category and 3D coordinates.

4. **Advanced Mapping (Optional)**:
   - Create a minimap using a canvas.
   - Display detected objects and player movements on the map.

5. **Moving Objects (Optional)**:
   - Use `NavMeshAgent` to make objects navigate dynamically.
   - Include data about moving objects in the LiDAR scan.

---

### **Additional Resources**
- [Unity NavMesh Documentation](https://docs.unity3d.com/Manual/nav-NavigationSystem.html)
- [Unity Raycasting Documentation](https://docs.unity3d.com/ScriptReference/Physics.Raycast.html)
- [LiDAR Simulator GitHub](https://github.com/ptibom/Lidar-Simulator)

---

Happy simulating with Unity!