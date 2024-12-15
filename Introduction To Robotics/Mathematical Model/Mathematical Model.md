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
- \(v\): Linear velocity  
- \(\omega\): Angular velocity  
- \(\Delta t\): Time step  

---

## **Implementation in Code**
- `robotPose` is updated using the equations:
  - **Horizontal zigzag:** \(x_{t+1}\) changes, \(y_t\) remains constant.  
  - **Vertical zigzag:** \(y_{t+1}\) changes, \(x_t\) remains constant.
