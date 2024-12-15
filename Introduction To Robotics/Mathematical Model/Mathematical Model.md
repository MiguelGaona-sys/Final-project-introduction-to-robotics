# Mathematical Model in the Code

The mathematical model of the vacuum robot is based on the principles of **path planning**, **navigation**, and **kinematics**, as outlined in **Chapters 5 and 6**. Below is a breakdown of the key components and their implementation in the code:

---

## **1. Path Planning**
Path planning ensures that the robot can efficiently navigate the environment while avoiding obstacles. The code leverages reactive navigation techniques and mathematical calculations for direction and movement:

### **Key Equations**
- **Obstacle Detection:**
  The Euclidean distance is used to determine if an obstacle is within the detection range:
  \[
  d = \sqrt{(x_{\text{current}} - x_{\text{obstacle}})^2 + (y_{\text{current}} - y_{\text{obstacle}})^2}
  \]
  Where:
  - \(x_{\text{current}}, y_{\text{current}}\): Robot's current position.
  - \(x_{\text{obstacle}}, y_{\text{obstacle}}\): Obstacle's position.
  - \(d\): Distance between the robot and the obstacle.

- **Reactive Behavior:**
  When an obstacle is detected (\(d < D_{\text{min}}\)), the robot changes direction by adjusting its orientation angle (\(\theta\)):
  \[
  \theta = \theta + \Delta \theta
  \]
  Where \(\Delta \theta\) is a random angle to ensure effective avoidance.

---

## **2. Navigation**
The robot's navigation is governed by **kinematic equations** that update its position over time.

### **Kinematic Model**
The robot’s position is updated based on its velocity (\(v\)), orientation (\(\theta\)), and time step (\(\Delta t\)):
- **X-Position:**
  \[
  x_{\text{new}} = x_{\text{current}} + v \cdot \cos(\theta) \cdot \Delta t
  \]
- **Y-Position:**
  \[
  y_{\text{new}} = y_{\text{current}} + v \cdot \sin(\theta) \cdot \Delta t
  \]

---

## **3. Cleaning Coverage**
The code tracks the cleaning coverage by updating a **binary grid map**, where:
- **0:** Represents uncleaned areas.
- **1:** Represents cleaned areas.

### **Cleaning Update:**
At each time step, the robot marks its current grid cell as cleaned:
\[
\text{cleaningMap}[x, y] = 1
\]

---

## **4. Obstacle Avoidance**
The robot employs a simple reactive navigation system to avoid obstacles:
- **Distance Threshold:** If an obstacle is detected within \(D_{\text{min}}\), the robot adjusts its orientation angle to avoid the obstacle.
- **Boundary Conditions:** To ensure the robot stays within the map limits, it reverses direction when reaching the edges of the map.

---

## **5. Efficiency Metrics**
The model includes mechanisms to optimize cleaning efficiency:
- **Cleaning Algorithms:** Spiral or zigzag patterns can be integrated to maximize cleaning coverage.
- **Energy Optimization:** By minimizing unnecessary movement, the robot conserves battery power.

---

### **Summary of Key Components**
| **Component**        | **Mathematical Equation/Logic**                                          | **Purpose**                        |
|-----------------------|-------------------------------------------------------------------------|------------------------------------|
| Obstacle Detection    | \(d = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}\)                           | Detects obstacles within range.    |
| Position Update       | \(x_{\text{new}}, y_{\text{new}}\) based on kinematics equations       | Updates robot's position.          |
| Cleaning Update       | \(\text{cleaningMap}[x, y] = 1\)                                      | Tracks cleaning progress.          |
| Orientation Adjustment| \(\theta = \theta + \Delta \theta\)                                   | Adjusts direction to avoid obstacles. |
| Boundary Condition    | Reverse direction at map edges                                        | Keeps the robot within boundaries. |

---

This mathematical model forms the foundation for the robot’s **navigation, cleaning, and obstacle avoidance capabilities**, ensuring an efficient and functional design.
