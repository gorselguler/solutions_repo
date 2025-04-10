# Investigating the Range as a Function of the Angle of Projection

## Motivation

Projectile motion is a foundational concept in mechanics. One important feature of projectile motion is the range, and how it changes with the angle of projection.

## 1. Theoretical Foundation

### Horizontal motion (x-direction)

x(t) = v₀ * cos(θ) * t


### Vertical motion (y-direction)

y(t) = v₀ * sin(θ) * t - (1/2) * g * t²



### Time of Flight (T)

T = (2 * v₀ * sin(θ)) / g



### Range (R)

R = v₀ * cos(θ) * T = (v₀² * sin(2θ)) / g

mathematica


## 2. Range as a Function of Launch Angle

R(θ) = (v₀² * sin(2θ)) / g

go

Maximum range occurs at:

θ = 45°

pgsql


## 3. Applications

- Ballistics  
- Sports  
- Engineering  

## 4. Python Code

```python
import numpy as np
import matplotlib.pyplot as plt

v0 = 20
g = 9.81
angles_deg = np.arange(0, 91, 1)
angles_rad = np.radians(angles_deg)
ranges = (v0 ** 2) * np.sin(2 * angles_rad) / g

plt.figure(figsize=(10, 5))
plt.plot(angles_deg, ranges, color='blue', linewidth=2)
plt.title("Projectile Range vs Launch Angle")
plt.xlabel("Launch Angle (degrees)")
plt.ylabel("Range (meters)")
plt.grid(True)
plt.axvline(45, color='red', linestyle='--', label='Max Range at 45°')
plt.legend()
plt.tight_layout()
plt.show()
