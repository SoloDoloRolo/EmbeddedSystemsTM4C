
# Embedded Systems TM4C Project

Welcome to the GitHub repository for my final project in Embedded Systems, utilizing the Texas Instruments TM4C123GH6PM microcontroller alongside predefined open-source software.

---


## **File Structure:**  
 - Core Functionality: PLL.c, PLL.h, tm4c123gh6pm.h enable the microcontroller’s operation.
 - Display: Nokia5110.c, Nokia5110.h, 48x84 Image.xls, and Nokia5110TestMain.c manage the LCD display.
 - Hardware: startup.s initializes hardware, and PCB layout.png ensures proper physical wiring.
 - Documentation: Nokia5110.pdf provide guidance and references.

---

## **Problem and Purpose**

This project began with a flash drive containing a partially implemented project riddled with errors and dead ends. Our objective: transform "Project 1.0" into a robust, optimized solution while collaborating as a team. 

**Challenges Identified:**
- The project wouldn’t load in KEIL IDE or onto the TM4C.
- Code flagged multiple errors (e.g., IntelliSense warnings).
- Presence of unused and commented-out code.
- Missing hardware components (motion sensors).

I took initiative to work through these challenges systematically, addressing issues piece by piece while documenting progress. While waiting for sensor deliveries, I began refactoring the codebase.

---

## **Project Workflow**

1. **Hardware Challenges:**  
   Collaborated with my lab partner, Xander, to wire the circuit on a breadboard. Initial issues arose when testing the motion sensors, which seemed non-functional. We:
   - Verified the sensors using a basic 5V circuit with an LED.
   - Discovered misconfigured potentiometers controlling sensitivity and delay.
   - Configuted the sensors for peak performance.

   ![Sensitivity Adjustment](https://github.com/user-attachments/assets/9c4f8e24-28be-4813-9be0-02d2a57e331c) 
   ![Delay Adjustment](https://github.com/user-attachments/assets/aaf639db-3281-4d1a-9de1-89e61374c7f8)

2. **Addressing Signal Conflicts:**  
   Separated input and output signals by assigning dedicated ports for motion sensors and alarms. Below is the port initialization code:

   ```c
   void PortB_Init(void){ 
       SYSCTL_RCGCGPIO_R |= 0x02;
       while ((SYSCTL_PRGPIO_R & 0x02) == 0);
       GPIO_PORTB_DIR_R = 0x21;
       GPIO_PORTB_DEN_R = 0x21;
   }

   void PortE_Init(void){ 
       SYSCTL_RCGCGPIO_R |= 0x10;
       while ((SYSCTL_PRGPIO_R & 0x10) == 0);
       GPIO_PORTE_DIR_R &= ~0x21;
       GPIO_PORTE_DEN_R |= 0x21;
   }
   ```

3. **Visual Output:**  
   Used the **Nokia5110** display to indicate the system state. The images were created using a 48x84 pixel matrix.




---

## **Alarm System States**

| **State**              | **Description**                  |
|-------------------------|----------------------------------|
| Home Safe              | No motion detected.             |
| Left Not Safe          | Motion detected on the left.    |
| Right Not Safe         | Motion detected on the right.   |
| Both Sides Not Safe    | Motion detected on both sides.  |

### Visual Representation of States:
![Home Safe](https://github.com/user-attachments/assets/235d8f09-c52e-43ec-8318-c55da0215511)
![Left Not Safe](https://github.com/user-attachments/assets/d6f9803c-da3f-4831-bfe2-a553bb029442)
![Right Not Safe](https://github.com/user-attachments/assets/9734f6ca-3499-4911-b579-2e4d5564e44b)
![Both Sides Not Safe](https://github.com/user-attachments/assets/d1c965a1-4a8f-4691-8416-542601155ef0)

---

## **Video Demo**

[Click here to watch the demo!](https://github.com/user-attachments/assets/e0b6dfd0-2cf4-453a-a37f-a14d5e0efec0)

---

## **Improvements Made**

- **Real-Time Feedback:** Tuned delays for smoother sensor operation.
- **Code Refactoring:** Improved modularity, readability, and maintainability.
- **Hardware Optimization:** Correctly configured motion sensor potentiometers.
- **Error Resolution:** Eliminated unused and buggy code.

---

## **Schematics and PCB Design**

Utilized **LTSpice** for schematic design and visualization:

- **3D Model Front View**  
  ![3D Model Front](https://github.com/user-attachments/assets/f21caf14-8c0c-4a85-a9a9-14cbc1e229fc)

- **PCB Schematic**  
  ![PCB Schematic](https://github.com/user-attachments/assets/9919168b-6fe8-4b66-93b3-dcfafa5b6ffe)

- **PCB Layout**  
  ![PCB Layout](https://github.com/user-attachments/assets/6e1a3bb1-2b57-44b0-bbae-40f0df5d37e8)

---

## **Acknowledgments**

Special thanks to **Jonathan Valvano** and his team for their foundational work in the development of `PLL.c` and the "Embedded Systems" book series. Their contributions significantly eased the integration and optimization process for this project. 

---
