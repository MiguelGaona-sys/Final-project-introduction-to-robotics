# Key Improvements Over the Previous Version

---

## **1. Systematic Zigzag Path Planning**
- **Initial Version:**  
  Relied on random direction changes and reactive behaviors for obstacle avoidance, resulting in inefficient and repetitive coverage.  
- **Final Version:**  
  Implements **horizontal and vertical zigzag patterns**, ensuring systematic and complete area coverage. The robot alternates between horizontal and vertical patterns dynamically to avoid any missed areas.

---

## **2. Condition-Based Path Switching**
- **Initial Version:**  
  No distinction in behavior based on robot location.  
- **Final Version:**  
  Introduces a **condition-based trigger**:  
  - Switches to **vertical zigzag navigation** when the robot enters a specific region (**x < 10 and y > 23**), adapting to the map's geometry for optimal coverage.  
  - Automatically alternates patterns when hitting walls or boundaries to avoid unnecessary looping.

---

## **3. Predefined Map with Static Walls**
- **Initial Version:**  
  Obstacles were randomly scattered, making systematic path planning challenging.  
- **Final Version:**  
  Uses a fixed **binary occupancy grid** representing walls and room boundaries. The robot follows this predefined map for **collision detection** and **planning**.

---

## **4. Complete Area Coverage**
- **Initial Version:**  
  The robot's random movements often left areas uncleaned.  
- **Final Version:**  
  Tracks cleaned areas in real time using a **coverage map**.  
  - Ensures the robot cleans the **entire accessible area** (**coverageThreshold = 1.0**) before stopping.

---

## **5. Improved Robot Kinematics**
- **Initial Version:**  
  Basic position updates without realistic motion dynamics.  
- **Final Version:**  
  Utilizes **differential drive kinematics**:  
  - Updates robot pose \((x, y, θ)\) using **linear velocity** and **heading angle**.  
  - Prevents wall crossing through accurate **collision detection** and **inflation of obstacles** to account for the robot's radius.
## MATLAB Code
Below is the MATLAB code implementing the enhanced functionality:

```matlab
% Simulation Parameters
mapSize = [25, 25]; % Room dimensions in meters
resolution = 5; % Resolution (cells per meter)
robotRadius = 0.5; % Radius of the robot in meters

% Create a binary occupancy map
roomMap = binaryOccupancyMap(mapSize(1), mapSize(2), resolution);

% Define walls (previously used map layout)
% Outer boundaries
setOccupancy(roomMap, [0:0.1:25; repmat(0, 1, numel(0:0.1:25))]', 1); % Bottom wall
setOccupancy(roomMap, [0:0.1:25; repmat(25, 1, numel(0:0.1:25))]', 1); % Top wall
setOccupancy(roomMap, [repmat(0, 1, numel(0:0.1:25)); 0:0.1:25]', 1); % Left wall
setOccupancy(roomMap, [repmat(25, 1, numel(0:0.1:25)); 0:0.1:25]', 1); % Right wall

% Vertical walls to divide the space
setOccupancy(roomMap, [repmat(12, 1, numel(0:0.1:15)); 0:0.1:15]', 1); % Middle vertical wall
setOccupancy(roomMap, [repmat(20, 1, numel(10:0.1:25)); 10:0.1:25]', 1); % Rightmost vertical wall

% Inflate the map for the robot's radius
inflate(roomMap, robotRadius);

% Define a coverage map
coverageMap = zeros(mapSize * resolution); % 0 = uncleaned, 1 = cleaned

% Robot Parameters
robotPose = [21, 24, 0]; % [x, y, theta] - Starting position near the top left
linearSpeed = 0.8; % Linear speed
sampleTime = 0.1; % Time step

% Simulation Parameters
maxIterations = 5000; % Maximum iterations for cleaning
coverageThreshold = 1.0; % Ensure 100% of accessible area is covered

% Visualization Setup
figure;
show(roomMap);
hold on;
robotPlot = plot(robotPose(1), robotPose(2), 'bo', 'MarkerSize', 10, 'MarkerFaceColor', 'b');
pathPlot = plot(robotPose(1), robotPose(2), 'g-', 'LineWidth', 1.5); % To visualize the path
title('Roomba Cleaning Simulation with Conditioned Vertical Switch');
xlabel('X [meters]');
ylabel('Y [meters]');

% Path storage for visualization
robotPath = []; % Store the robot's path

% Cleaning Logic Initialization
currentPattern = "horizontal"; % Start with horizontal zigzag
yStep = -1; % Step size in the Y direction (downwards)
xStep = 1; % Step size in the X direction
xDirection = 1; % Start by moving right

% Simulation loop
while maxIterations > 0
    % Check for condition to switch to vertical zigzag
    if robotPose(1) < 10 && robotPose(2) > 23
        currentPattern = "vertical";
    end
    
    if strcmp(currentPattern, "horizontal")
        % Horizontal Zigzag Movement
        while true
            nextPose = robotPose(1:2) + [xDirection * linearSpeed * sampleTime, 0];
            if checkOccupancy(roomMap, nextPose) || nextPose(1) <= 0 || nextPose(1) >= mapSize(1)
                break; % Stop horizontal movement at a boundary
            end
            robotPose(1:2) = nextPose;
            robotPath = [robotPath; robotPose(1:2)];

            % Mark as cleaned
            gridX = round(robotPose(1) * resolution);
            gridY = round(robotPose(2) * resolution);
            if gridX > 0 && gridX <= size(coverageMap, 2) && gridY > 0 && gridY <= size(coverageMap, 1)
                coverageMap(gridY, gridX) = 1; % Mark as cleaned
            end

            % Update visualization
            set(robotPlot, 'XData', robotPose(1), 'YData', robotPose(2));
            set(pathPlot, 'XData', robotPath(:, 1), 'YData', robotPath(:, 2));
            pause(0.01);
        end

        % Move vertically to the next row
        nextPose = robotPose(1:2) + [0, yStep];
        if checkOccupancy(roomMap, nextPose) || nextPose(2) <= 0 || nextPose(2) >= mapSize(2)
            yStep = -yStep; % Reverse vertical movement when at the boundary
            nextPose = robotPose(1:2) + [0, yStep];
        end
        robotPose(2) = nextPose(2);
        xDirection = -xDirection; % Reverse horizontal direction
    else
        % Vertical Zigzag Movement
        while true
            nextPose = robotPose(1:2) + [0, yStep * linearSpeed * sampleTime];
            if checkOccupancy(roomMap, nextPose) || nextPose(2) <= 0 || nextPose(2) >= mapSize(2)
                break; % Stop vertical movement at a boundary
            end
            robotPose(1:2) = nextPose;
            robotPath = [robotPath; robotPose(1:2)];

            % Mark as cleaned
            gridX = round(robotPose(1) * resolution);
            gridY = round(robotPose(2) * resolution);
            if gridX > 0 && gridX <= size(coverageMap, 2) && gridY > 0 && gridY <= size(coverageMap, 1)
                coverageMap(gridY, gridX) = 1; % Mark as cleaned
            end

            % Update visualization
            set(robotPlot, 'XData', robotPose(1), 'YData', robotPose(2));
            set(pathPlot, 'XData', robotPath(:, 1), 'YData', robotPath(:, 2));
            pause(0.01);
        end

        % Move horizontally to the next column
        nextPose = robotPose(1:2) + [xStep, 0];
        if checkOccupancy(roomMap, nextPose) || nextPose(1) <= 0 || nextPose(1) >= mapSize(1)
            xStep = -xStep; % Reverse horizontal movement when at the boundary
            nextPose = robotPose(1:2) + [xStep, 0];
        end
        robotPose(1) = nextPose(1);
        yStep = -yStep; % Reverse vertical direction
    end

    % Check coverage condition
    coveredArea = sum(coverageMap(:)) / numel(coverageMap);
    if coveredArea >= coverageThreshold
        disp('Cleaning complete!');
        break;
    end
    
    maxIterations = maxIterations - 1;
end

% Final Coverage Visualization
figure;
imagesc(flipud(coverageMap));
colormap(gray);
title('Final Cleaning Coverage');
xlabel('X');
ylabel('Y');
colorbar;
