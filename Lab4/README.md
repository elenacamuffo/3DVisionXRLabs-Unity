# Unity Lab 4: 3D Meshes, Point Clouds & Shaders

*By Elena Camuffo, PhD Student*  
_A.Y. 2022/2023_

---

### **Overview**

This lab explores key concepts in 3D data representation, including meshes, point clouds, and shaders. It covers rendering techniques, shader programming, and tools for manipulating point cloud data.

---

### **3D Data Representations**

3D data can be represented in several forms:

1. **Point Clouds**:
   - Set of 3D points defined by coordinates (x, y, z).
   - Attributes like color, intensity, or labels can also be included.
   - Commonly acquired from LiDAR or other reality capture devices.

2. **Meshes**:
   - Collection of vertices, edges, and faces defining the shape of a polyhedral object.
   - Common formats: **Face-Vertex Mesh** and **Vertex-Vertex Mesh**.
   - Supports UV mapping, vertex attributes, and tangent vectors.

3. **Shaders**:
   - Used to calculate rendering effects, like light and shadow, during the rendering pipeline.

---

### **Point Clouds**

#### **Formats**
- Point clouds can be stored in formats like `.OFF`, `.OBJ`, `.PLY`, and `.FBX`.
- Complex to render directly; often converted to meshes for visualization.

#### **Tools for Point Cloud Processing**
- [PCUtils Repository](https://github.com/Dan8991/PCutils): Python tools for point cloud processing.

---

### **Rendering with Shaders**

Shaders are programs that run on the GPU and determine the appearance of objects in a scene. Unity supports several types:

1. **Surface Shaders**:
   - Simplify the process of writing lit shaders.

2. **Unlit Shaders**:
   - Do not interact with Unity’s lighting system; ideal for special effects.

3. **Image Effect Shaders**:
   - Applied as post-processing effects.

#### **Shader Script Example**

```csharp
Shader "Custom/VertexColor"
{
    Properties
    {
        _PointSize("PointSize", Float) = 10
    }
    SubShader
    {
        Pass
        {
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag

            struct VertexInput
            {
                float4 v : POSITION;
                float4 color : COLOR;
            };

            struct VertexOutput
            {
                float4 pos : SV_POSITION;
                float size : PSIZE;
                float4 col : COLOR;
            };

            VertexOutput vert(VertexInput v)
            {
                VertexOutput o;
                o.pos = UnityObjectToClipPos(v.v);
                o.size = _PointSize;
                o.col = v.color;
                return o;
            }

            float4 frag(VertexOutput o) : COLOR
            {
                return o.col;
            }
            ENDCG
        }
    }
}
```
- **Vertex Shader**: Handles transformations of vertices in the 3D model.
- **Fragment Shader**: Calculates pixel colors.

---

### **Shader Graph Tool**

For a node-based approach to creating shaders, Unity provides the Shader Graph tool.

#### **Steps**
1. Install the **Universal Rendering Pipeline (URP)**.
2. Enable Shader Graph in Unity’s package manager.
3. Use nodes to define shader behavior and preview real-time effects.

---

### **Lab Exercise: Visualization Tool**

#### **Objective**
Use shaders and point cloud tools to create unique visual effects and convert data formats.

#### **Steps**
1. **Set Up URP**:
   - Test the point cloud meshing tool in Unity.
   - Configure the Universal Rendering Pipeline renderer.

2. **Build Point Cloud Shader**:
   - Use Shader Graph to create a shader that gives point clouds a neon-like appearance.

3. **Create a Mesh Shader**:
   - Write a custom shader to make meshes appear holographic, with transparency and motion effects.

4. **Advanced Features**:
   - Parse `.txt` point cloud data from LiDAR and convert it to `.OFF` format.
   - Visualize the parsed data as a mesh.

5. **Optional Challenge**:
   - Use LiDAR point clouds from the simulator.
   - Assign colors based on object labels or distances.

---

### **Additional Resources**
- [Unity Shader Graph](https://unity.com/shader-graph)
- [PCUtils Repository](https://github.com/Dan8991/PCutils)
- [Shader Graph Video Tutorial](https://www.youtube.com/watch?v=VsUK9K6UbY4)

---

Happy rendering and experimenting with Unity!

