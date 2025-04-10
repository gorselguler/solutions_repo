# Problem 2
# Investigating the Dynamics of a Forced Damped Pendulum

## Motivation
The forced damped pendulum is a classic system in nonlinear dynamics. Whether in mechanical clocks, playground swings, or scientific experiments, it exhibits rich behaviors: resonance, damping, and even chaos. Understanding this system provides foundational insights into more complex real-world phenomena.

---

## 1. Theoretical Foundation

The motion of a forced damped pendulum is governed by the second-order nonlinear differential equation:

$$
\frac{d^2\theta}{dt^2} + \beta \frac{d\theta}{dt} + \omega_0^2 \sin(\theta) = A \cos(\omega t)
$$

Where:

- \( \theta \): Angular displacement  
- \( \beta \): Damping coefficient  
- \( \omega_0 \): Natural frequency  
- \( A \): Driving amplitude  
- \( \omega \): Driving frequency  

### Small-Angle Approximation

For small angles we can approximate \( \sin(\theta) \approx \theta \), making the equation linear:

$$
\frac{d^2\theta}{dt^2} + \beta \frac{d\theta}{dt} + \omega_0^2 \theta = A \cos(\omega t)
$$

---

### Resonance

Resonance occurs when the driving frequency equals the system's natural frequency with respect to the damping:

$$
\omega = \sqrt{\omega_0^2 - \frac{\beta^2}{2}}
$$

---

## 2. Analysis of Dynamics

### Time Evolution

The angular position over time can be numerically solved via methods like Euler or Runge-Kutta:

$$
\theta'' = -\beta \theta' - \omega_0^2 \sin(\theta) + A \cos(\omega t)
$$

---

### Parametric Effects

- **Damping (\( \beta \))**: Reduces amplitude over time; suppresses chaotic behavior.  
- **Driving (\( A \), \( \omega \))**: Influences oscillation strength and possible resonance.  

---

### Transition to Chaos

As demonstrated by Strogatz and others, the forced pendulum becomes chaotic in specific amplitude and frequency ranges.  
Key signs include:
- Aperiodic behavior  
- Extreme sensitivity to initial conditions  

---

## 3. Practical Applications

- **Engineering Oscillators**: Used to tune systems from car suspensions to mechanical energy harvesters.  
- **Neuroscience Models**: Similar equations appear in neuron spiking (Hodgkin-Huxley model).  
- **Clocks & Timekeeping**: Historical use in accurate mechanical oscillators.  

---

## 4. Implementation

### Python Simulation Outline

```python
import numpy as np
import matplotlib.pyplot as plt

# Parameters
beta = 0.25
omega0 = 1.5
A = 1.2
omega = 0.667

# Time settings
dt = 0.04
t_max = 60
t = np.arange(0, t_max, dt)

# Initialization
theta = np.zeros_like(t)
omega_dot = np.zeros_like(t)
theta[0] = 0.2  # Initial angle

# Simulation loop (Euler method)
for i in range(1, len(t)):
    omega_dot[i] = omega_dot[i-1] + dt * (-beta * omega_dot[i-1] - omega0**2 * np.sin(theta[i-1]) + A * np.cos(omega * t[i-1]))
    theta[i] = theta[i-1] + dt * omega_dot[i]

# Plotting
plt.figure(figsize=(10,4))
plt.plot(t, theta, label="θ(t)")
plt.title("Damped Driven Pendulum Simulation")
plt.xlabel("Time (s)")
plt.ylabel("Angle (rad)")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()
