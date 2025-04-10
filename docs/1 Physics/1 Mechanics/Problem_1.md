# Problem 1
# Investigating the Range as a Function of the Angle of Projection

## 🎯 Motivation

Projectile motion is a foundational concept in mechanics, where equations of motion can be used to understand the motion of objects under uniform acceleration. One important feature of projectile motion is the **range**, and how it changes with the **angle of projection**.

---

## 1. 🧠 Theoretical Foundation

### Horizontal motion (x-direction):

The horizontal motion is uniform (no acceleration):
x(t) = v₀ * cos(θ) * t

csharp
Copy
Edit

### Vertical motion (y-direction):

The vertical motion is uniformly accelerated:
y(t) = v₀ * sin(θ) * t - (1/2) * g * t²

pgsql
Copy
Edit

### Time of Flight (T):

We calculate time when the object returns to y = 0:
T = (2 * v₀ * sin(θ)) / g

csharp
Copy
Edit

### Range (R):

Plug T into the horizontal motion:
R = v₀ * cos(θ) * T = (v₀² * sin(2θ)) / g

yaml
Copy
Edit

---

## 2. 📈 Analysis of the Range

### Range as a Function of the Launch Angle

The function is:
R(θ) = (v₀² * sin(2θ)) / g

yaml
Copy
Edit
- Maximum range is achieved at **θ = 45°** because **sin(2θ)** reaches its maximum at **2θ = 90°**.

---

## 3. ⚙️ Practical Applications

- Ballistics
- Sports Science (soccer, basketball, etc.)
- Engineering (throwing mechanics)

---
## 4. Limitations and Suggestions for Improvements:

**The current model assumes:**

- No air resistance, which isn't realistic for most real-world projectiles.  
- Flat ground, neglecting any effects of terrain variation.  
- Constant gravitational acceleration, which isn’t accurate for higher altitudes or other celestial bodies.  

**To improve the model, you could:**

- Incorporate air resistance using drag equations to model the deceleration of the projectile.  
- Account for varying terrain by modifying the initial and final conditions of the projectile’s path.  
- Consider varying gravity for different planetary conditions (e.g., Mars, Moon).  

**Conclusion:**  
Through this task, we explored the fundamental principles of projectile motion and derived the governing equations. By analyzing how the range depends on the launch angle, initial velocity, and gravity, we gained insight into both the physics and practical applications of projectile motion. The implementation of a simulation further enhances the understanding by visualizing the relationships and behaviors. Finally, by reflecting on the limitations of the idealized model, we identified possible improvements for more accurate real-world modeling.

---

![Projectile Range as a Function of Launch Angle](path-to-your-image/projectile-range-graph.png)

*Projectile Range as a Function of Launch Angle*

## 5. 💻 Implementation (Python Code)

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
v0 = 20  # Initial velocity (m/s)
g = 9.81  # Gravitational acceleration (m/s^2)

# Angle range from 0° to 90°
angles_deg = np.arange(0, 91, 1)
angles_rad = np.radians(angles_deg)

# Compute range for each angle
ranges = (v0 ** 2) * np.sin(2 * angles_rad) / g

# Plotting
plt.figure(figsize=(10, 5))
plt.plot(angles_deg, ranges, color='royalblue', linewidth=2)
plt.title("Projectile Range vs Launch Angle")
plt.xlabel("Launch Angle (degrees)")
plt.ylabel("Range (meters)")
plt.grid(True)
plt.axvline(45, color='red', linestyle='--', label='Max Range at 45°')
plt.legend()
plt.tight_layout()
plt.show()

