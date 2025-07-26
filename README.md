

#  Robot Navigation with Pygame

This project simulates a robot navigating a 2D environment to reach randomly placed targets using angular heuristics. It uses `Pygame` for rendering, and the logic simulates a simple agent-based system where the robot selects actions based on its relative orientation to the target.

---

##  Features

- Random initialization of robot and target positions
- Robot pose updates based on wheel angular velocities
- Angle-based decision-making for navigation
- Reward and penalty system to guide behavior
- Full graphical simulation with wheel visualization
- Modular function definitions for easy extension (e.g., Q-learning)

---

##  How It Works

### 1. **Environment Setup**
- Screen dimensions: 800 x 600
- Robot and target objects are placed randomly within a rectangular field.
- Robot has three wheels (at 60°, 180°, and 300°).

### 2. **Functions**
- `new_episode()`: Starts a new episode with random robot/target positions and angle.
- `clip()`: Utility to restrict values (not currently used).
- `update_pose()`: Calculates the next pose (x, y, theta) based on wheel speeds and robot orientation.

### 3. **Main Loop Logic**
- The simulation runs in a continuous loop using Pygame.
- The robot computes the angle between itself and the target.
- Based on the quadrant of the target, one of four action states is selected.
- The robot moves toward the target; it gets:
  - **+10 points** if it reaches the target,
  - **-10 points** if it leaves the field,
  - **-0.01 penalty** per step to encourage quicker solutions.

### 4. **Rendering**
- Robot, target, and wheels are visualized using Pygame.
- Wheels are color-coded:
  - Red = 60°, Magenta = 180°, Blue = 300°
- Score, steps, and episode count are displayed at the top right.

---

##  Technologies Used

- Python
- Pygame
- Math (trigonometry for angle and vector rotation)

---

##  Getting Started

### Prerequisites
```bash
pip install pygame
```

### Run the Simulation
```bash
python robot_navigation.py  # or run the notebook interactively
```

---

##  Potential Extensions

- Integrate Q-learning or Deep Q Networks (DQN)
- Track episode history for training
- Add collision detection with obstacles
- Use rewards to train a neural agent

---

##  Author

**Andrew Khaleski Opata**  
[LinkedIn](https://www.linkedin.com/in/andrew-khaleski-opata-a932b2183)  

