# Unity Lab 6: Reinforcement Learning and ML Agents

*By Elena Camuffo, PhD Student*  
_A.Y. 2022/2023_

---

### **Overview**

This lab explores the Unity ML-Agents Toolkit, an open-source plugin that enables simulations and games to serve as environments for training intelligent agents. Topics include reinforcement learning, imitation learning, and training intelligent behaviors.

---

### **Unity ML-Agents Toolkit**

#### **Key Learning Methods**
1. **Reinforcement Learning (RL)**:
   - Agents learn through trial and error, receiving positive or negative rewards based on their actions.

2. **Imitation Learning**:
   - Agents learn by imitating the actions demonstrated by a human player.

#### **Components of RL**
- **State (S)**: The current situation of the agent as returned by the environment.
- **Action (A)**: The set of all possible moves the agent can take.
- **Reward (R)**: Feedback from the environment after taking an action.
- **Policy (π)**: The agent’s strategy to decide actions based on its current state.
- **Value (V)**: The long-term expected return from a state.
- **Q-Value (Q)**: The expected return from a state-action pair.

---

### **Installation**

To set up ML-Agents:
1. Create a virtual environment:
   ```bash
   py -m venv venv
   venv\Scripts\activate
   python -m pip install --upgrade pip
   pip install torch
   pip install mlagents
   ```
2. Install the **ML-Agents** package in Unity:
   - Open Unity’s Package Manager.
   - Enable preview packages and install version 1.9 preview.

---

### **Agent Behavior Parameters**

The **Behavior Parameters** component is essential for creating agents:
- **Model**: Holds the neural network model used for inference.
- **Behavior Type**:
  1. **Default**: Agent learns autonomously via RL.
  2. **Heuristic**: Agent is guided by user input.
  3. **Inference**: Agent uses a pre-trained model to act.
- **Decision Requester Module**: Allows agents to decide which action to take.
- **Ray Perception Sensor**: Simulates the agent’s perception of its surroundings.

---

### **Agent Script Example**

Below is an example of an ML-Agent script:

```csharp
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;

public class RollerAgent : Agent
{
    Rigidbody rBody;

    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }

    public Transform Target;

    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }

        Target.localPosition = new Vector3(Random.value * 8 - 4, 0.5f, Random.value * 8 - 4);
    }

    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }

    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * 10);

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);

        if (distanceToTarget < 1.42f)
        {
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }
    }

    public override void Heuristic(in ActionBuffers actionsOut)
    {
        var continuousActionsOut = actionsOut.ContinuousActions;
        continuousActionsOut[0] = Input.GetAxis("Horizontal");
        continuousActionsOut[1] = Input.GetAxis("Vertical");
    }
}
```

---

### **Training Your Agent**

To train an agent, use the terminal with the `mlagents-learn` command:
```bash
mlagents-learn config/ConfigFile.yaml --run-id=<run-name>
```
- Duplicate environments to accelerate training.
- Monitor progress with TensorBoard:
  ```bash
  tensorboard --logdir=<log-directory> --port=8080
  ```

---

### **Imitation Learning**

- Use the **Demonstration Recorder** to record player actions for the agent to imitate.
- Techniques include:
  - **Generative Adversarial Imitation Learning (GAIL)**: Discriminator guesses if trajectories are from the agent or a demo.
  - **Behavioral Cloning**: Agent replicates recorded actions.

---

### **Lab Exercise: Xmas Agents**

#### **Objective**
Set up and train agents to solve tasks using reinforcement and imitation learning.

#### **Steps**
1. **Install ML-Agents**:
   - Set up the environment as described in the installation section.

2. **Complete the Agent Script**:
   - Implement missing functions in the script.

3. **Set Up the Environment**:
   - Test heuristic configurations.
   - Create and duplicate prefabs of the environment for training.

4. **Train Your Model**:
   - Start training and monitor progress with TensorBoard.

5. **Test Your Model**:
   - Assign the trained model to the agent and evaluate its performance.

6. **Optional**:
   - Record agent behavior for imitation learning and adjust parameters to train a more complex task.

---

### **Additional Resources**
- [Unity ML-Agents GitHub Repository](https://github.com/Unity-Technologies/ml-agents)
- [Introduction to Deep RL](https://thomassimonini.medium.com/an-introduction-to-deep-reinforcement-learning-17a565999c0c)
- [Unity ML-Agents Documentation](https://unity-technologies.github.io/ml-agents/)

---

Happy training and experimenting with Unity ML-Agents!

