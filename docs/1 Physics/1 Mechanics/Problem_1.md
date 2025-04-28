# 🎯 Investigating the Range as a Function of the Angle of Projection

![Projectile Motion](https://upload.wikimedia.org/wikipedia/commons/3/3e/Projectile_Motion.png)

## 🚀 Problem Overview

Investigate how the **range** of a projectile depends on its **launch angle** under ideal conditions:
- No air resistance
- Constant gravitational acceleration

---

## 📚 Theoretical Foundation

The projectile's motion splits into two components:

- **Horizontal displacement**:
  \[
  x(t) = v_0 \cos(\theta) t
  \]
- **Vertical displacement**:
  \[
  y(t) = v_0 \sin(\theta) t - \frac{1}{2} g t^2
  \]

Where:
- \( v_0 \) = initial velocity
- \( \theta \) = launch angle
- \( g \) = gravitational acceleration (9.81 m/s²)

**Total time of flight** when \( y = 0 \):

\[
t = \frac{2v_0 \sin(\theta)}{g}
\]

Thus, the **range** \( R \) is:

\[
R = \frac{v_0^2 \sin(2\theta)}{g}
\]

> 🧠 **Key Result**: Maximum range occurs when \( \theta = 45^\circ \).

---

## 📈 Python Simulation

Use the following code to simulate and plot the projectile range vs launch angle:

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # m/s²
v0 = 20   # initial velocity (m/s)

# Angle range
angles = np.linspace(0, 90, 500)
ranges = (v0**2) * np.sin(np.deg2rad(2*angles)) / g

# Plotting
plt.figure(figsize=(10,6))
plt.plot(angles, ranges, 'b-', linewidth=2)
plt.title('Projectile Range vs Launch Angle', fontsize=16)
plt.xlabel('Launch Angle (degrees)', fontsize=14)
plt.ylabel('Range (meters)', fontsize=14)
plt.grid(True)
plt.show()
