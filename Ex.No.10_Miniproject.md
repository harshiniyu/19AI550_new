# Ex.No: 10  Implementation of 2D/3D game 
                                                                          
### REGISTER NUMBER : 212223240050
### GAME NAME: bird 
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
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Slingshot : MonoBehaviour
{
    public LineRenderer[] lineRenderers;
    public Transform[] stripPositions;
    public Transform center;
    public Transform idlePosition;

    public Vector3 currentPosition;
    public float maxLength;
    public float bottomBoundary;
    bool isMouseDown;
    public GameObject birdPrefab;
    public float birdPositionOffset;
    Rigidbody2D bird;
    Collider2D birdCollider;
    public float force;

    void Start()
    {
        lineRenderers[0].positionCount = 2;
        lineRenderers[1].positionCount = 2;
        lineRenderers[0].SetPosition(0, stripPositions[0].position);
        lineRenderers[1].SetPosition(0, stripPositions[1].position);
        CreateBird();
    }

    void CreateBird()
    {
        bird = Instantiate(birdPrefab).GetComponent<Rigidbody2D>();
        birdCollider = bird.GetComponent<Collider2D>();
        birdCollider.enabled = false;
        bird.bodyType = RigidbodyType2D.Kinematic;
        ResetStrips();
    }

    void Update()
    {
        if (isMouseDown)
        {
            Vector3 mousePosition = Input.mousePosition;
            mousePosition.z = 10;
            currentPosition = Camera.main.ScreenToWorldPoint(mousePosition);
            currentPosition = center.position + Vector3.ClampMagnitude(currentPosition - center.position, maxLength);
            currentPosition = ClampBoundary(currentPosition);
            SetStrips(currentPosition);

            if (birdCollider)
                birdCollider.enabled = true;
        }
        else
        {
            ResetStrips();
        }
    }

    private void OnMouseDown() => isMouseDown = true;

    private void OnMouseUp()
    {
        isMouseDown = false;
        Shoot();
        currentPosition = idlePosition.position;
    }

    void Shoot()
    {
        bird.bodyType = RigidbodyType2D.Dynamic;
        Vector3 birdForce = (currentPosition - center.position) * force * -1;
        bird.linearVelocity = birdForce;

        bird.GetComponent<Bird>().Release();

        bird = null;
        birdCollider = null;
        Invoke("CreateBird", 2);
    }

    void ResetStrips()
    {
        currentPosition = idlePosition.position;
        SetStrips(currentPosition);
    }

    void SetStrips(Vector3 position)
    {
        lineRenderers[0].SetPosition(1, position);
        lineRenderers[1].SetPosition(1, position);

        if (bird)
        {
            Vector3 dir = position - center.position;
            bird.transform.position = position + dir.normalized * birdPositionOffset;
            bird.transform.right = -dir.normalized;
        }
    }

    Vector3 ClampBoundary(Vector3 vector)
    {
        vector.y = Mathf.Clamp(vector.y, bottomBoundary, 1000);
        return vector;
    }
}


using UnityEngine;

public class Bird : MonoBehaviour
{
    private Rigidbody2D rb;

    void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    public void Release()
    {
        // This will be called from the Slingshot when you release the bird
        // You can add extra behavior here like enabling a trail, sounds, etc.
        Debug.Log("Bird released!");
    }
}
bird.cs


```
### Output:
![WhatsApp Image 2025-11-12 at 08 19 02_77812928](https://github.com/user-attachments/assets/614b1596-90e9-4216-9e35-1767a85614e2)


### Result:
Thus the game was developed using Unity and adopted _-----------AI technology.
