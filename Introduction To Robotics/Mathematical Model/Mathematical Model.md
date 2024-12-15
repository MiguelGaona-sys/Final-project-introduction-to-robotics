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

\[
M'(x, y) =
\begin{cases} 
1 & \text{if } \sqrt{(x - x_{\text{wall}})^2 + (y - y_{\text{wall}})^2} \leq r \\
0 & \text{otherwise}
\end{cases}
\]

---

### **Implementation in Code:**
- `binaryOccupancyMap` is used to define the room.  
- `inflate` function ensures the inflated safety margin around walls and obstacles.
