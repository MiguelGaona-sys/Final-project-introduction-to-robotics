# Pseudocode: Roomba Robot Simulation with Zigzag Path Planning

## **Initialization**
1. **Set Room Parameters:**
   - Define room dimensions `mapSize` and resolution.
   - Set `robotRadius` for collision safety.

2. **Create Binary Occupancy Map:**
   - Set outer walls and static vertical walls.
   - Inflate walls by `robotRadius` for safety.

3. **Initialize Coverage Map:**
   - `coverageMap` is a grid to track cleaned cells.

4. **Robot Parameters:**
   - Initial pose: `robotPose = [x, y, θ]`.
   - Set `linearSpeed` and `sampleTime`.

5. **Visualization Setup:**
   - Display the room map.
   - Initialize robot and path visualization.

---

## **Simulation Logic**
- **Set Initial Pattern:**  
   `currentPattern = "horizontal"`

- **Initialize Movement Variables:**  
   - `yStep`: Vertical step direction (-1).  
   - `xStep`: Horizontal step direction (1).  
   - `xDirection`: Horizontal movement direction (right).

### **Simulation Loop (Until maxIterations or full coverage):**
1. **Check Condition to Switch to Vertical Zigzag:**
   - If `robotPose.x < 10` and `robotPose.y > 23` → Switch to `vertical` pattern.

2. **Zigzag Movement:**
   - **If currentPattern = "horizontal":**
     - Move horizontally while no obstacle is detected:
       - Update `robotPose.x`.
       - Mark cell as cleaned in `coverageMap`.
       - Update visualization.
     - Stop at boundary and move vertically by `yStep`.
     - Reverse `xDirection` for the next horizontal pass.

   - **If currentPattern = "vertical":**
     - Move vertically while no obstacle is detected:
       - Update `robotPose.y`.
       - Mark cell as cleaned in `coverageMap`.
       - Update visualization.
     - Stop at boundary and move horizontally by `xStep`.
     - Reverse `yStep` for the next vertical pass.

3. **Check for Cleaning Completion:**
   - Calculate cleaned area percentage:  
     \[
     \text{coveredArea} = \frac{\text{number of cleaned cells}}{\text{total cells}}
     \]
   - If `coveredArea >= coverageThreshold`, stop the simulation.

4. **Decrement `maxIterations` Counter.**

---

## **End of Simulation**
1. Display message: `"Cleaning complete!"`
2. Visualize the final coverage map.

---

## **Notes:**
- **Collision Detection:**  
   Uses `checkOccupancy()` to check for obstacles and walls.
- **Boundary Handling:**  
   Reverses directions (`xStep`, `yStep`, `xDirection`) to avoid crossing walls.
- **Visualization:**  
   Updates robot’s path in real-time and displays a final cleaned map.

