# Autonomous House-Cleaning Robot (Enhanced Version)

## Project Overview
This is an improved version of the **Autonomous House-Cleaning Robot** project. It extends the first implementation by introducing **obstacle simulation** and minor refinements to enhance its performance. The robot now avoids predefined obstacles on the map while maintaining its cleaning trajectory and updating the cleaning status in real time.

---

## Key Enhancements
1. **Obstacle Simulation:**
   - Randomly placed obstacles are added to the map to test the robot's obstacle avoidance capabilities.
   - The robot uses a reactive strategy to change direction when obstacles are detected within a specific range.

2. **Path Visualization:**
   - The robot's path is visualized as it moves, allowing for better debugging and analysis.

3. **Cleaning Map:**
   - The cleaning status of the environment is tracked and displayed visually at the end of the simulation.

---

## Mathematical Model
This implementation still incorporates concepts from **Reactive Navigation** and **Map-Based Planning**, while introducing obstacle avoidance strategies. Key mathematical elements include:

### 1. **Reactive Navigation:**
   - Obstacle detection is performed using the Euclidean distance formula:
     \[
     d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}
     \]
   - If \(d < D_{\text{min}}\), the robot changes direction by turning at a random angle.

### 2. **Kinematic Model:**
   - Position updates are calculated using:
     \[
     x_{t+1} = x_t + v \cos(\theta) \cdot \Delta t
     \]
     \[
     y_{t+1} = y_t + v \sin(\theta) \cdot \Delta t
     \]

---

## MATLAB Code
Below is the MATLAB code implementing the enhanced functionality:

```matlab
% Configuration
mapSize = [100, 100]; % Room dimensions
cleaningMap = zeros(mapSize); % Cleaning status (0 = dirty, 1 = cleaned)
x = 10; y = 10; % Initial position
theta = rand * 2 * pi; % Random initial orientation
v = 1; % Linear velocity
omega = pi / 4; % Angular velocity (45 degrees per second)
D_min = 5; % Obstacle detection range
numIterations = 1000; % Simulation steps
dt = 1; % Time step

% Initialize path storage
pathX = x; % Store x-coordinates of the path
pathY = y; % Store y-coordinates of the path

% Visualization setup
figure;
hold on;
axis([0 mapSize(2) 0 mapSize(1)]);
xlabel('X Position');
ylabel('Y Position');
title('Roomba Cleaning Simulation with Path');
robotPlot = plot(x, y, 'bo', 'MarkerSize', 8, 'MarkerFaceColor', 'b'); % Robot position
pathPlot = plot(pathX, pathY, 'k-', 'LineWidth', 1); % Path visualization

% Obstacle configuration (random obstacles for demonstration)
obstacles = [30, 40; 70, 20; 50, 80]; % Example obstacles
scatter(obstacles(:,1), obstacles(:,2), 100, 'r', 'filled'); % Visualize obstacles

% Simulation loop
for t = 1:numIterations
    % Update cleaning map
    gridX = round(x); gridY = round(y);
    if gridX > 0 && gridY > 0 && gridX <= mapSize(2) && gridY <= mapSize(1)
        cleaningMap(gridY, gridX) = 1; % Mark as cleaned
    end
    
    % Check for obstacles
    obstacleDetected = false;
    for i = 1:size(obstacles, 1)
        dist = norm([x, y] - obstacles(i, :));
        if dist < D_min
            obstacleDetected = true;
            break;
        end
    end
    
    % Reactive behavior
    if obstacleDetected
        theta = theta + (rand - 0.5) * pi; % Turn away from obstacle
    elseif rand < 0.1 % Random direction change occasionally
        theta = theta + (rand - 0.5) * pi / 2;
    end
    
    % Update position based on kinematics
    x = x + v * cos(theta) * dt;
    y = y + v * sin(theta) * dt;
    
    % Boundary conditions (avoid leaving map)
    if x < 1 || y < 1 || x > mapSize(2) || y > mapSize(1)
        theta = theta + pi; % Turn around
        x = max(min(x, mapSize(2)), 1);
        y = max(min(y, mapSize(1)), 1);
    end
    
    % Store the path
    pathX = [pathX, x];
    pathY = [pathY, y];
    
    % Update visualization
    set(robotPlot, 'XData', x, 'YData', y); % Update robot position
    set(pathPlot, 'XData', pathX, 'YData', pathY); % Update path
    pause(0.05);
end
hold off;

% Visualization of cleaning status
figure;
imagesc(flipud(cleaningMap));
colormap(gray);
colorbar;
title('Cleaning Map');
xlabel('X');
ylabel('Y');
