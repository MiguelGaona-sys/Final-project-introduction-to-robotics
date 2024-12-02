# Autonomous House-Cleaning Robot

## Project Overview
This project demonstrates the design and simulation of an **Autonomous House-Cleaning Robot** using concepts from **Reactive Navigation**, **Map-Based Planning**, and **Localization**. The robot navigates and cleans an indoor environment while avoiding obstacles, utilizing mathematical models and advanced algorithms.

---

## Key Features
- **Reactive Navigation:** Inspired by biological behaviors (e.g., Braitenberg Vehicles), the robot reacts dynamically to its environment.
- **Map-Based Path Planning:** Implements techniques like **Probabilistic Roadmap (PRM)** and **Rapidly-Exploring Random Trees (RRT)** for efficient navigation.
- **Localization:** Utilizes **Dead Reckoning** and **Monte Carlo Localization** to estimate the robot's position.
- **Simulation:** Implemented and visualized in MATLAB with CAD models for physical representation.

---

## Mathematical Model
The mathematical models used are based on chapters 5 and 6 of the course:

### 1. **Reactive Navigation**
- The robot uses sensor-based feedback to adjust its path dynamically.
- Inspired by Braitenberg Vehicles and simple automata, the robot performs goal-seeking and obstacle avoidance using environmental stimuli.

### 2. **Map-Based Planning**
- **Probabilistic Roadmap Method (PRM):** Samples the configuration space and connects nodes to create a feasible path.
- **Rapidly-Exploring Random Trees (RRT):** Generates kinematically feasible paths by sampling random configurations.

### 3. **Localization Techniques**
- **Dead Reckoning:** Estimates position using odometry and heading.
- **Monte Carlo Localization:** Maintains multiple hypotheses to handle sensor noise and uncertainty.

---

## MATLAB Implementation
Below is the core MATLAB code used for simulating the robot's navigation and obstacle avoidance.

```matlab
% Configuration setup
mapSize = [100, 100]; % Cleaning area size
map = zeros(mapSize); % Initialize empty map
goal = [80, 80]; % Target position
x = 10; y = 10; % Initial position
theta = rand * 2 * pi; % Random initial orientation
v = 1; % Robot speed
D_min = 5; % Minimum distance to detect an obstacle

% Visualization setup
figure;
hold on;
axis([0 mapSize(2) 0 mapSize(1)]);
xlabel('Position X');
ylabel('Position Y');
title('Robot Navigation Simulation');

% Simulation loop
for t = 1:1000 % Number of iterations
    % Update position
    x = x + v * cos(theta);
    y = y + v * sin(theta);

    % Check for obstacles and adjust direction
    if detectObstacle(x, y, D_min, map)
        theta = theta + (rand - 0.5) * pi; % Random direction change
    end

    % Plot current position
    plot(x, y, 'bo'); % Blue dots for position
    pause(0.05); % Pause for visualization
end
hold off;

% Obstacle detection function
function isObstacle = detectObstacle(x, y, D_min, map)
    % Ensure coordinates are within map bounds
    if x < D_min || y < D_min || x > size(map, 2) - D_min || y > size(map, 1) - D_min
        isObstacle = true; % Detect edges as obstacles
    else
        isObstacle = false; % No obstacle detected
    end
end

