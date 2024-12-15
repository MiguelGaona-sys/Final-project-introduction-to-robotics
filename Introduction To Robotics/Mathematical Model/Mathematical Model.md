# Mathematical Model in the Code

The mathematical model of the robot is based on the principles of **path planning**, **navigation**, and **kinematics**, as outlined in **Chapters 5 and 6**. Below is an explanation of the key components:
# 1. Room Representation (Binary Occupancy Grid)

**Concepts Used (Chapters 5 and 6):**
- **Binary Occupancy Grid:** The room is modeled as a 2D grid where each cell is either occupied (1) or free (0).  
- **Inflation:** The walls and obstacles are inflated by the robot's radius to account for collision safety.

---

### **Mathematical Model:**
- The grid is represented as \( M(x, y) \), where \( M(x, y) = 1 \) indicates a wall or obstacle, and \( M(x, y) = 0 \) indicates a free space.  
- Inflation ensures that the robot does not come closer than its radius \( r \) to any wall, represented as:

![image](https://github.com/user-attachments/assets/52592e14-8280-4960-a29c-6a91a73cd873)


---

### **Implementation in Code:**
- `binaryOccupancyMap` is used to define the room.  
- `inflate` function ensures the inflated safety margin around walls and obstacles.
# 2. Robot's Pose Representation

**Concepts Used (Chapter 6):**
- **Pose:** The robot's state is represented as a 3-tuple \((x, y, θ)\), where \(x, y\) are the robot's coordinates, and \(θ\) is its orientation (heading angle).

---

## **Mathematical Model**
- The robot's position and orientation are updated using the **differential drive kinematic equations**:

![image](https://github.com/user-attachments/assets/ab5888a8-5a1a-4e4c-8792-66e6425a4663)


**Where:**
- \(ν\): Linear velocity  
- \(Ω\): Angular velocity  
- \(Δ t\): Time step  

---

## **Implementation in Code**
- `robotPose` is updated using the equations:
- **Horizontal zigzag:** x<sub>t+1</sub> changes, y<sub>t</sub> remains constant.  
- **Vertical zigzag:** y<sub>t+1</sub> changes, x<sub>t</sub> remains constant.
# 3. Path Planning (Zigzag Patterns)

**Concepts Used (Chapter 5):**
- **Systematic Coverage:**  
  The zigzag path (both horizontal and vertical) ensures systematic coverage without revisiting the same area unnecessarily.
- **Boundary Handling:**  
  Boundary detection ensures the robot reverses direction when hitting walls, ensuring all accessible areas are covered.

---

## **Mathematical Model**

### 1. **Horizontal Zigzag**
- The robot moves horizontally until it detects a boundary (collision).  
- The vertical position changes by **Δy = ±1** at the end of each horizontal pass:  

\[
x<sub>t+1</sub> = x<sub>t</sub> + v · Δt
\]
\[
y<sub>t+1</sub> = y<sub>t</sub> + Δy<sub>step</sub>
\]

- **x<sub>direction</sub>** reverses upon hitting a boundary.

---

### 2. **Vertical Zigzag**
- The robot moves vertically until it detects a boundary (collision).  
- The horizontal position changes by **Δx = ±1** at the end of each vertical pass:

\[
y<sub>t+1</sub> = y<sub>t</sub> + v · Δt
\]
\[
x<sub>t+1</sub> = x<sub>t</sub> + Δx<sub>step</sub>
\]

- **y<sub>direction</sub>** reverses upon hitting a boundary.

---

## **Implementation in Code**

Horizontal and vertical zigzag behaviors are alternated dynamically using:

```matlab
if robotPose(1) < 10 && robotPose(2) > 23
    currentPattern = "vertical";
end
```
This logic ensures the robot switches patterns as necessary to achieve full coverage.
# 4. Collision Detection

**Concepts Used (Chapter 5):**
- **Obstacle Avoidance:**  
  The robot checks for collisions using the occupancy grid.  
- **Boundary Handling:**  
  The robot detects when it reaches the edges of the room and reverses direction or switches patterns.

---

## **Mathematical Model**
- Collision detection is based on:

![image](https://github.com/user-attachments/assets/2f006012-e845-4232-9d0b-57af85e07f64)


- Here, **M'**(x<sub>next</sub>, y<sub>next</sub>) is the **inflated occupancy grid value** at the robot's next position.

---

## **Implementation in Code**
- `checkOccupancy(roomMap, nextPose)` is used to determine if the robot's next position will result in a collision.
# 5. Coverage Completion

**Concepts Used (Chapters 5 and 6):**
- **Coverage Metrics:**  
  The simulation ensures cleaning stops only when 100% of the accessible area is covered.
- **Grid Updates:**  
  The robot marks each grid cell as cleaned upon visiting it.

---

## **Mathematical Model**
- Cleaning percentage is calculated as:

\[
\text{Coverage} = \frac{\sum M_{\text{cleaned}}(x, y)}{\text{Total Grid Cells}}
\]

where \( M_{\text{cleaned}}(x, y) = 1 \) for cleaned cells.

---

## **Implementation in Code**
- The robot updates the `coverageMap`:

```matlab
gridX = round(robotPose(1) * resolution);
gridY = round(robotPose(2) * resolution);
coverageMap(gridY, gridX) = 1;

