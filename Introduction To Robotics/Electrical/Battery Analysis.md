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
\text{Current (I)} = \frac{\text{Power (P)}}{\text{Voltage (V)}} = \frac{12\,\text{W}}{12\,\text{V}} = 1\,\text{A}.
\]

### **Total Current for Two Motors**
\[
1\,\text{A} \times 2 = 2\,\text{A}.
\]

### **Runtime for Wheel Motors**
A **13500mAh battery (13.5Ah)** can power the wheels for:  
\[
\text{Runtime (hours)} = \frac{\text{Battery Capacity (Ah)}}{\text{Current (I)}} = \frac{13.5\,\text{Ah}}{2\,\text{A}} = 6.75\,\text{hours}.
\]

---

## **3. Power Consumption of Brush Motors**
### **Typical Setup**
- Two brush motors.  
- Power consumption per motor: **5W**.

### **Power Draw per Motor**
At **12V**, a **5W motor** draws:  
\[
\text{Current (I)} = \frac{\text{Power (P)}}{\text{Voltage (V)}} = \frac{5\,\text{W}}{12\,\text{V}} = 0.4166\,\text{A}.
\]

### **Total Current for Two Motors**
\[
0.4166\,\text{A} \times 2 = 0.833\,\text{A}.
\]

### **Runtime for Brush Motors**
A **13500mAh battery (13.5Ah)** can power the brush motors for:  
\[
\text{Runtime (hours)} = \frac{\text{Battery Capacity (Ah)}}{\text{Current (I)}} = \frac{13.5\,\text{Ah}}{0.833\,\text{A}} = 16.2\,\text{hours}.
\]

---

## **4. Power Consumption of Suction Motor**
### **Typical Setup**
- One suction motor.  
- Power consumption: **30W**.

### **Power Draw per Motor**
At **12V**, a **30W motor** draws:  
\[
\text{Current (I)} = \frac{\text{Power (P)}}{\text{Voltage (V)}} = \frac{30\,\text{W}}{12\,\text{V}} = 2.5\,\text{A}.
\]

### **Runtime for Suction Motor**
A **13500mAh battery (13.5Ah)** can power the suction motor for:  
\[
\text{Runtime (hours)} = \frac{\text{Battery Capacity (Ah)}}{\text{Current (I)}} = \frac{13.5\,\text{Ah}}{2.5\,\text{A}} = 5.4\,\text{hours}.
\]

---

## **5. Combined Power Consumption**
If the suction motor, wheel motors, and brush motors are powered by the same **13500mAh battery**, the total runtime depends on the combined current draw:

### **Total Current Draw Estimate**
- **Suction Motor:** 2.5A.  
- **Wheel Motors:** 2A.  
- **Brush Motors:** 0.833A.  

### **Total Current**
\[
I_{\text{total}} = 2.5\,\text{A} + 2\,\text{A} + 0.833\,\text{A} = 5.33\,\text{A}.
\]

### **Runtime with 13500mAh Battery**
\[
\text{Runtime (hours)} = \frac{\text{Battery Capacity (Ah)}}{\text{Total Current (I)}} = \frac{13.5\,\text{Ah}}{5.33\,\text{A}} = 2.5\,\text{hours}.
\]

---

## **Conclusion**
The **13500mAh battery** is sufficient for powering the suction motor, wheel motors, and brush motors for approximately **2.5 hours** of operation.  
For longer runtime, a higher-capacity battery is recommended.
