# Ex.No: 3  Basic movements in Unity 
### DATE: 22.08.2025                                                                         
### REGISTER NUMBER : 212223240050
### AIM: 
 To learn the basic movements translation,scaling and rotation of game objects through code.
### Procedure:
1. Setup the Scene
2. Open Unity and create a 3D Scene.
3. Add three objects:Cube → Rename to Object1 (for movement),Sphere → Rename to Object2 (for rotation).Capsule → Rename to Object3 (for scaling).
4. Add the Script,Create a C# Script → Name it TransformOperations.cs.
5. Write the code for translation,scaling and rotation,save and close the script
6. Save the script
7. Select any empty GameObject (or create one: GameObject → Create Empty).
8. Attach the TransformOperations script to it.
9. In the Inspector, assign Object1 → Drag the Cube,Object2 → Drag the Sphere.Object3 → Drag the Capsule.
10. Run the Scene Press Play ▶️ in Unity
11. Stop the program.
### Program 
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ob : MonoBehaviour
{
    public Transform o1;
    public Transform o2;
    public Transform o3;

    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        o1.Translate(0.2f, 0, 0);
        o2.Rotate(0.2f, 0, 0);
        o3.localScale += new Vector3(0, 0.2f, 0);
    }
}
```
### Output:

<img width="1393" height="710" alt="Screenshot 2025-08-22 134323" src="https://github.com/user-attachments/assets/26cf402b-45b1-48d5-8229-7ca6bbeae1bd" />

<img width="1335" height="712" alt="Screenshot 2025-08-22 134405" src="https://github.com/user-attachments/assets/e7fcc524-1a68-48c9-b1dc-dacc455a420e" />






### Result:
Thus the basic movement is learned through scripting


