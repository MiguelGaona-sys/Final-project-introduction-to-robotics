# Pseudocode: Reactive Navigation with Cleaning Simulation (logic of the code)

### **1. Initialize Environment:**
- Define room dimensions as a 2D grid (`mapSize`).
- Set all grid cells as dirty (`0 = dirty`, `1 = cleaned`).
- Place robot at an initial position `(x, y)` with a random orientation (`theta`).
- Define simulation parameters:
  - Velocity (`v`).
  - Angular velocity (`omega`).
  - Time step (`dt`).
  - Obstacle detection range (`D_min`).

---

### **2. Set Obstacles:**
- Randomly place obstacles in the room (coordinates stored in `obstacles`).

---

### **3. Initialize Visualization:**
- Create a plot to display:
  - The robot's position.
  - Path.
  - Obstacles.
- Use markers to dynamically show:
  - The robot.
  - Its cleaning path.

---

### **4. Begin Simulation Loop (for a fixed number of iterations):**
1. **Update Cleaning Map:**
   - Mark the robot's current position as cleaned.

2. **Obstacle Detection:**
   - Check the distance to all obstacles.
   - If an obstacle is within the detection range:
     - Set `obstacleDetected = True`.
   - Otherwise, proceed as normal.

3. **Reactive Behavior:**
   - If an obstacle is detected:
     - Change orientation (`theta`) to avoid collision (randomized).
   - Occasionally introduce random direction changes for better coverage.

4. **Update Position Using Kinematics:**
   - Calculate the new position `(x, y)` based on current velocity and orientation.

5. **Boundary Conditions:**
   - Ensure the robot stays within the room:
     - Adjust orientation and position if it moves out of bounds.

6. **Store and Update Path:**
   - Append the new position to the path history for visualization.

7. **Update Visualization:**
   - Refresh the robot’s position and path on the plot.

---

### **5. Post-Simulation Visualization:**
- Display the final cleaning map with:
  - Cleaned areas.
  - Uncleaned areas.

---
