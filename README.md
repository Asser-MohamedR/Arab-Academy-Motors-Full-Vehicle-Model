# 14 DoF Full Vehicle Mathematical Model in Simulink

**Author:** Asser Mohamed Abdelalim  

## 1. Project Overview
This repository contains a robust, modular 14 Degree of Freedom (DoF) full vehicle handling dynamics model implemented in MATLAB/Simulink. The core kinematics and governing differential equations are adapted from the mathematical framework detailed in Ghike, C., & Shim, T. (2006). 14 Degree-of-Freedom Vehicle Model for Roll Dynamics study. SAE Technical Papers on CD-ROM/SAE Technical Paper Series, 1. https://doi.org/10.4271/2006-01-1277 . 

While the theoretical foundation of the vehicle body dynamics relies on established literature[cite: 164, 328], the primary engineering contribution of this project is the translation of these complex, coupled systems into a solver-efficient computational environment. Additionally, a custom powertrain subsystem and a data-fitted Pacejka tire model were developed independently to complete the vehicle architecture. This model was utilized by our engineering team to simulate vehicle behavior and transient responses under various dynamic steering conditions.

## 2. Mathematical Framework
The mathematical model captures the spatial dynamics of the vehicle by allocating the 14 degrees of freedom into two main categories:

* **Sprung Mass (6 DoF):** Captures the motion of the vehicle body, specifically the longitudinal, lateral, and vertical velocities, alongside the roll, pitch, and yaw angular movements.
* **Unsprung Mass (8 DoF):** Captures the independent dynamics of the four wheels, accounting for the vertical velocity and rotational speed of each individual tire.

## 3. Original Subsystem Development & Integration
To complete the full vehicle model and ensure highly realistic dynamic responses, the following subsystems were developed from scratch and integrated into the primary 14 DoF architecture:

* **Custom Powertrain Model:** Developed to provide realistic longitudinal torque inputs to the driven wheels. This subsystem interfaces directly with the wheel spin degrees of freedom, ensuring accurate acceleration and engine braking dynamics without relying on generic Simulink powertrain blocks.
* **Pacejka Magic Formula Tire Data Fitting:** To accurately capture the highly non-linear nature of tire-road interactions, a custom tire model was implemented. Raw tire data was computationally processed and fitted to extract the four core coefficients of the Pacejka Magic Formula. This approach ensured that the lateral and longitudinal tire forces—critical inputs to the sprung mass equations—were highly representative of real-world tire behavior. *(Note: See `[insert filename.png]` for the data fitting curve).*

## 4. Simulink System Architecture
The model is designed with a strong emphasis on modularity and code readability, preventing algebraic loops and managing the stiff dynamics inherent to vehicle suspension and tire relaxation systems. 

Key subsystems include:
* **Steering Mechanism:** Converts driver steering wheel inputs into independent front-right and front-left tire steer angles using Ackerman geometry principles[cite: 210].
* **Tire Model:** Calculates transient forces based on the custom-fitted Pacejka equations[cite: 219].
* **Body Kinematics:** Computes the 6 DoF state variables of the sprung mass using external and inertial forces[cite: 308].
* **Wheel Spin:** Determines the rotational dynamics of each corner based on powertrain torque and longitudinal tire friction[cite: 325, 326].

## 5. Prerequisites and Execution
To run this simulation, you will need:
* MATLAB & Simulink (Version `[Insert Version, e.g., R2022b]` or newer).
* No additional specialized toolboxes are required.

**How to Run and Configure:**
1. Open MATLAB and navigate to the repository directory.
2. Open the primary Simulink model `[insert model name, e.g., FullVehicleModel.slx]`.
3. **Configure Parameters:** The model is designed with a highly integrated, user-friendly masked interface. Simply double-click the main vehicle subsystem block to open the parameter mask. From this dialog box, you can directly view and edit all physical vehicle data (e.g., sprung mass, moments of inertia, suspension stiffness, and geometric dimensions) without needing to run external initialization scripts.
4. Click **Run** to execute the simulation. 
5. Standard scopes are pre-configured within the model to output key dynamic responses such as Yaw Rate, Lateral Acceleration, and Roll Angle over time.

## References
* Ibrahim, M. S., Abdelaziz, M., Elmarhoomy, A., & Ghoniema, M. (2018). *A 14 DEGREES OF FREEDOM VEHICLE DYNAMICS MODEL TO PREDICT THE BEHAVIOR OF A GOLF CAR*. Proceedings of the 18th Int. [cite_start]AMME Conference[cite: 7, 8].
