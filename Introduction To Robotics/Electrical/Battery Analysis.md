# Power Consumption and Battery Analysis
 
---

## **1. Separate Powering for Efficiency**
- **Why:**  
  The suction motor, wheel motors, and brush motors serve different functions with varying power requirements:
  - **Suction Motor:** Requires steady power for airflow and debris collection (e.g., 30W or more).  
  - **Wheel Motors:** Require significantly less power (e.g., 12W per motor) for mobility.  
  - **Brush Motors:** Require even less power (e.g., 5W per motor).  

- **Impact:**  
  Separating the systems allows optimized power allocation, ensuring the robot performs all functions efficiently.

---

## **2. Power Consumption of Wheel Motors**
To estimate if the **13500mAh battery** is sufficient for powering the wheel motors:

### **Typical Setup**
- Two servo motors for differential drive (one for each wheel).  
- Power consumption per motor: **12W**.

### **Power Draw per Motor**
At **12V**, a **12W motor** draws:  
\[
Current (I) = Power (P)/ Voltage (V) = 12W/12V = 1A
\]

### **Total Current for Two Motors**
\[
1 A×2= 2 A.
\]

### **Runtime for Wheel Motors**
A **13500mAh battery (13.5Ah)** can power the wheels for:  
\[
Runtime ( Hours ) = Battery capacity (Ah)/Current (I) = 13.5(Ah)/2A = 6.75 hours.
\]

---

## **3. Power Consumption of Brush Motors**
### **Typical Setup**
- Two brush motors.  
- Power consumption per motor: **5W**.

### **Power Draw per Motor**
At **12V**, a **5W motor** draws:  
\[
Current (I) = Power (P)/ Voltage (V) = 5W/12V = 0.4166A
\]

### **Total Current for Two Motors**
\[
0.4166 A×2= 0.833 A.
\]

### **Runtime for Brush Motors**
A **13500mAh battery (13.5Ah)** can power the brush motors for:  
\[
Runtime ( Hours ) = Battery capacity (Ah)/Current (I) = 13.5(Ah)/0.833A = 16.2 hours.
\]

---

## **4. Power Consumption of Suction Motor**
### **Typical Setup**
- One suction motor.  
- Power consumption: **30W**.

### **Power Draw per Motor**
At **12V**, a **30W motor** draws:  
\[
Current (I) = Power (P)/ Voltage (V) = 30W/12V = 2.5A
\]

### **Runtime for Suction Motor**
A **13500mAh battery (13.5Ah)** can power the suction motor for:  
\[
Runtime ( Hours ) = Battery capacity (Ah)/Current (I) = 13.5(Ah)/2.5A = 5.4hours
\]

---

## **5. Combined Power Consumption**
If the suction motor, wheel motors, and brush motors are powered by the same **13500mAh battery**, the total runtime depends on the combined current draw:

### **Total Current Draw Estimate**
- **Suction Motor:** I= 30W/12V = 2.5A.  
- **Wheel Motors:** 2A.  
- **Brush Motors:** 0.833A.  

### **Total Current**
\[
I(total) = 2.5A + 2A + 0.8333= 5.33A
\]

### **Runtime with 13500mAh Battery**
\[
Runtime(real) = 13.5Ah/ 5.33A = 2.5 hours.
\]

---

## **Conclusion**
The **13500mAh battery** is sufficient for powering the suction motor, wheel motors, and brush motors for approximately **2.5 hours** of operation.  
For longer runtime, a higher-capacity battery is recommended.
