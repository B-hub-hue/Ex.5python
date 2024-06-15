# Ex.5python
i added two of my exercise for this project
# Define the system of differential equations
def system(t, y, r1, r2, alpha12, alpha21, K1, K2):
    P1, P2 = y
    dP1dt = r1 * P1 * (1 - P1 + alpha12 * P2 / K1)
    dP2dt = r2 * P2 * (1 - P2 + alpha21 * P1 / K2)
    return [dP1dt, dP2dt]

# Parameters
r1 = 0.1
r2 = 0.2
alpha12 = 0.1
alpha21 = 0.1
K1 = 100
K2 = 100

# Initial conditions
P1_0 = 50
P2_0 = 50
y0 = [P1_0, P2_0]

# Time span
t_span = (0, 100)

# Solve the system of differential equations
sol = solve_ivp(system, t_span, y0, args=(r1, r2, alpha12, alpha21, K1, K2), t_eval=np.linspace(0, 100, 1000))

# Plot the results
plt.figure(figsize=(12, 6))

# Population vs. time
plt.subplot(2, 2, 1)
plt.plot(sol.t, sol.y[0], label="Species 1")
plt.plot(sol.t, sol.y[1], label="Species 2")
plt.xlabel("Time")
plt.ylabel("Population")
plt.legend()


# Trajectory in parameter space

plt.subplot(2, 2, 2)
plt.plot(sol.y[0], sol.y[1])
plt.xlabel("Species 1 Population")
plt.ylabel("Species 2 Population")
plt.title("Trajectory in Parameters Space")
