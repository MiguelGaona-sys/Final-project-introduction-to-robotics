# Conclusion and Discussion

## **Conclusion**
The vacuum cleaning robot achieves an efficient and intelligent cleaning system by integrating **systematic path planning**, **differential drive kinematics**, and **optimized power management**. The robot successfully:

- Implements **horizontal and vertical zigzag patterns** for systematic and complete area coverage.
- Utilizes a **13500mAh battery**, which powers the suction motor, wheel motors, and brush motors for approximately **2.5 hours** of combined operation.
- Ensures effective **collision detection** and obstacle avoidance using a predefined binary occupancy grid and real-time feedback.
- Tracks cleaning performance through a **coverage map**, ensuring 100% cleaning of accessible areas before stopping.

This combination of features demonstrates the robot's reliability and efficiency in navigating complex environments while maintaining optimized power consumption.

---

## **Discussion**
### **1. Systematic Path Planning**
The implementation of **zigzag movement patterns** significantly improves cleaning efficiency compared to random movements. The robot switches between horizontal and vertical patterns dynamically, ensuring systematic coverage and reducing redundant passes. The use of **condition-based triggers** allows the robot to adapt its behavior to specific regions, optimizing performance for various map geometries.

### **2. Power Management and Runtime**
The separation of power systems for the suction motor, wheel motors, and brush motors allows optimized power allocation:
- **Wheel Motors:** Operate at 12W per motor for mobility.  
- **Brush Motors:** Consume only 5W per motor for cleaning assistance.  
- **Suction Motor:** Requires 30W to generate adequate suction force for debris collection.

With a **13500mAh battery**, the robot achieves approximately **2.5 hours** of runtime under combined loads (5.33A current draw). While this runtime is sufficient for household cleaning, future improvements, such as higher-capacity batteries or power-efficient components, could further extend operation time.

### **3. Collision Detection and Obstacle Avoidance**
The use of a **binary occupancy grid** and **inflated obstacle margins** ensures the robot avoids collisions with walls and obstacles. Real-time feedback from sensors enables the robot to reverse or adjust direction dynamically when detecting boundaries, contributing to smoother navigation and enhanced safety.

### **4. Key Trade-offs**
While the current design achieves reliable performance, certain trade-offs exist:
- **Battery Life vs. Suction Power:** Increasing suction motor power improves cleaning efficiency but reduces runtime.
- **Cleaning Speed vs. Coverage Accuracy:** Faster movements may reduce cleaning thoroughness, while slower movements ensure complete coverage at the cost of time.

Balancing these trade-offs is essential for future iterations of the robot.

### **5. Future Improvements**
To further enhance performance, the following improvements could be considered:
- Integration of **advanced sensors** (e.g., LiDAR or camera-based SLAM) for more precise navigation and real-time mapping.
- Use of **higher-capacity batteries** or energy-efficient motors to extend runtime.
- Implementation of **adaptive cleaning algorithms** to optimize paths based on the environment and dirt detection.

---

