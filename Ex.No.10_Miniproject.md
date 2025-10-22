# Ex.No: 10  Implementation of 2D/3D game 
                                                                          
### REGISTER NUMBER : 212223240050
### GAME NAME: Maze Runner  
### AIM: 

To develop a Unity 3D game where an AI-controlled agent uses reinforcement learning (via Unity ML-Agents) to autonomously navigate through a maze and reach a designated goal, demonstrating basic principles of artificial intelligence in games.


### Algorithm:
```
1.Setup Unity ML-Agents:

Install Unity and ML-Agents Toolkit.

Create a new 3D project.

Import ML-Agents package into Unity.
2.Design the Environment:

Add a Plane as the ground.

Create a simple maze using 3D Cubes as walls.
Add a Sphere as the goal object.
3.Create the Agent:

Add a Capsule as the player.
Attach Rigidbody and create a C# script MazeAgent.cs.
Define observation space, actions, and reward functions.
4.Agent Logic:

Reward agent for reaching the target.

Penalize for time consumption or wall collisions.

Randomize the goal position each episode.
4.Training:

Configure Behavior Parameters.

Use Heuristic mode for manual testing.

Optionally train with mlagents-learn command.
5.Testing & Output:

Run the game in Unity.

Observe the agent learning and navigating the maze.
```  
### Program:
```
using Unity.MLAgents;
using Unity.MLAgents.Actuators;
using Unity.MLAgents.Sensors;
using UnityEngine;

public class MazeAgent : Agent
{
    public Transform target;
    private Rigidbody agentRb;

    public override void Initialize()
    {
        agentRb = GetComponent<Rigidbody>();
    }

    public override void OnEpisodeBegin()
    {
        this.transform.localPosition = new Vector3(-4, 0.5f, -4);
        agentRb.velocity = Vector3.zero;

        target.localPosition = new Vector3(Random.Range(-4, 4), 0.5f, Random.Range(-4, 4));
    }

    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(target.localPosition);
        sensor.AddObservation(agentRb.velocity.x);
        sensor.AddObservation(agentRb.velocity.z);
    }

    public override void OnActionReceived(ActionBuffers actions)
    {
        float moveX = actions.ContinuousActions[0];
        float moveZ = actions.ContinuousActions[1];

        Vector3 move = new Vector3(moveX, 0, moveZ);
        agentRb.AddForce(move * 10f);

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, target.localPosition);

        if (distanceToTarget < 1.5f)
        {
            SetReward(1.0f);
            EndEpisode();
        }

        AddReward(-0.001f);
    }

    public override void Heuristic(in ActionBuffers actionsOut)
    {
        var continuousActionsOut = actionsOut.ContinuousActions;
        continuousActionsOut[0] = Input.GetAxis("Horizontal");
        continuousActionsOut[1] = Input.GetAxis("Vertical");
    }
}
```
### Output:

![image](https://github.com/user-attachments/assets/8340c190-57cf-4240-bfbc-ad55dddd5271)

### Result:
Thus the game was developed using Unity and adopted _-----------AI technology.
