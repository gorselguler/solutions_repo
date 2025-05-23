# Problem 3

# # Trajectories of a Freely Released Payload Near Earth

## Motivation
The trajectory of an object released from a moving rocket depends on its initial velocity and the gravitational influence of Earth. By analyzing these trajectories, we can understand orbital insertion, reentry paths, or escape scenarios. This knowledge is essential in space mission planning, satellite deployment, and reentry vehicle design.

---

## Physics Background

### Newton's Law of Gravitation:

$$
F = \frac{GMm}{r^2} \Rightarrow a = \frac{GM}{r^2} 
$$

This acceleration acts towards the center of Earth.

### Types of Trajectories
- **Circular Orbit**: Object moves with constant speed in a circular path.
- **Elliptical Orbit**: Object is bound to Earth but not at a constant distance.
- **Parabolic Escape**: Minimum speed to escape Earth's gravity.
- **Hyperbolic Escape**: Object escapes Earth with excess velocity.
- **Suborbital Trajectory**: Falls back to Earth before completing an orbit.

---

### Initial Conditions and Solver
```python
# Choose an altitude and initial velocity (vary this to simulate different cases)
altitude = 300e3  # 300 km
r0 = R_earth + altitude
v_circular = np.sqrt(mu / r0)  # Circular orbital speed

# Modify initial velocity to simulate different trajectories
initial_conditions = {
    'suborbital': [0, 0.7 * v_circular],
    'circular': [0, v_circular],
    'elliptical': [0, 1.1 * v_circular],
    'escape': [0, np.sqrt(2) * v_circular],
}

fig, ax = plt.subplots(figsize=(8, 8))

for label, vy0 in initial_conditions.items():
    y0 = [r0, 0, 0, vy0]  # x, vx, y, vy
    sol = solve_ivp(equations, [0, 10000], y0, t_eval=np.linspace(0, 10000, 5000))
    x = sol.y[0]
    y = sol.y[2]
    ax.plot(x / 1e3, y / 1e3, label=label)

# Earth
earth = plt.Circle((0, 0), R_earth / 1e3, color='blue', alpha=0.3)
ax.add_patch(earth)

ax.set_xlabel('x (km)')
ax.set_ylabel('y (km)')
ax.set_title('Payload Trajectories near Earth')
ax.set_aspect('equal')
ax.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```
![Trajectory Image](image69.png)

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Constants
mu = 3.986e14        # Earth's gravitational parameter (m^3/s^2)
R_earth = 6371e3     # Earth's radius (m)

# Equations of motion
def equations(t, y):
    x, vx, y_pos, vy = y
    r = np.sqrt(x**2 + y_pos**2)
    ax = -mu * x / r**3
    ay = -mu * y_pos / r**3
    return [vx, ax, vy, ay]

# Earth impact event detection
def hit_earth(t, y):
    x, _, y_pos, _ = y
    r = np.sqrt(x**2 + y_pos**2)
    return r - R_earth  # zero when reaching Earth's surface

hit_earth.terminal = True
hit_earth.direction = -1  # trigger only when approaching Earth

# Initial altitude (300 km above Earth surface)
altitude = 300e3
r0 = R_earth + altitude
x0 = r0
y0 = 0
vx0 = 0

# Velocities in km/s converted to m/s
velocities_kms = np.arange(5.5, 13.5, 0.5)
velocities_ms = velocities_kms * 1e3

# Plot setup
fig, ax = plt.subplots(figsize=(8, 8))

for v in velocities_ms:
    initial_state = [x0, vx0, y0, v]
    sol = solve_ivp(
        equations,
        [0, 10000],
        initial_state,
        t_eval=np.linspace(0, 10000, 5000),
        events=hit_earth,
        rtol=1e-8,
        atol=1e-10
    )
    x = sol.y[0]
    y = sol.y[2]
    ax.plot(x / 1e3, y / 1e3, label=f'{v/1e3:.1f} km/s')

# Draw the Earth
earth = plt.Circle((0, 0), R_earth / 1e3, color='blue', alpha=0.3)
ax.add_patch(earth)

# Plot labels and settings
ax.set_xlabel('x (km)')
ax.set_ylabel('y (km)')
ax.set_title('Orbits with Different Initial Velocities (Impact Stopping)')
ax.set_aspect('equal')
ax.legend(loc='upper right', fontsize='small')
plt.grid(True)
plt.tight_layout()
plt.show()
```

![Trajectory Image](colabimage1.png)



---

## Applications in Space Missions
- **Orbital Insertion**: Matching circular or elliptical orbits for satellites.
- **Escape Trajectory**: Interplanetary missions (e.g., to Mars).
- **Reentry Design**: Predicting where a returning capsule will land.

---

## Conclusion
By changing the initial velocity of a payload, we observe distinct paths that help classify motion near Earth. Simulating these paths enhances our understanding of celestial mechanics and supports mission-critical decisions in aerospace engineering.

```python
radii = np.linspace(R_earth, R_earth + 2e6, 500)
v_orbit = np.sqrt(mu / radii) / 1e3      # km/s
v_escape = np.sqrt(2 * mu / radii) / 1e3 # km/s

plt.figure(figsize=(8, 5))
plt.plot((radii - R_earth) / 1e3, v_orbit, label='Orbital Velocity')
plt.plot((radii - R_earth) / 1e3, v_escape, label='Escape Velocity')
plt.xlabel('Altitude (km)')
plt.ylabel('Velocity (km/s)')
plt.title('Velocity vs Altitude Near Earth')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```
![alt text](image-5.png)

```python
x = np.linspace(-2e7, 2e7, 40)
y = np.linspace(-2e7, 2e7, 40)
X, Y = np.meshgrid(x, y)
R = np.sqrt(X**2 + Y**2)
ax = -mu * X / R**3
ay = -mu * Y / R**3

plt.figure(figsize=(7, 7))
plt.streamplot(X/1e6, Y/1e6, ax, ay, color=np.sqrt(ax**2 + ay**2), cmap='plasma')
earth = plt.Circle((0, 0), R_earth / 1e6, color='blue', alpha=0.3)
plt.gca().add_patch(earth)
plt.xlabel('X (10⁶ m)')
plt.ylabel('Y (10⁶ m)')
plt.title('Gravitational Vector Field Around Earth')
plt.grid(True)
plt.axis('equal')
plt.show()
```

![alt text](image-6.png)



