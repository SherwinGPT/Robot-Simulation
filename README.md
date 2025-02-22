      
# Robot Simulation

TLDR: 
1. Install the requirements in the Requirements.txt file.
2. Run `Robot_Simulation.py` as is. Wait for each simulation to finish before closing. The graphs will generate after the simulations.


## Description
This project simulates a robot vacuum cleaner operating in a rectangular room, which can be either empty or furnished. 
The simulation models the cleaning process, tracks the percentage of the room cleaned over time, and allows comparison of different robot 
cleaning strategies.  The project includes implementations for:

*   **`StandardRobot`:**  A robot that moves in a straight line until it encounters a wall or furniture, at which point it randomly changes direction.
*   **`FaultyRobot`:**  A robot that has a probability of randomly changing direction at each time step, *and* may fail to clean the tile it's on.
*   **Empty and Furnished Rooms:** Different room types that affect robot navigation.
*   **Visualization**: A tkinter based visualization tool to see the robots cleaning.
*   **Performance Analysis:** Functions to run simulations and generate plots comparing the performance of different robot types and room configurations.


## Table of Contents
- [Robot Simulation](#robot-simulation)
  - [Description](#description)
  - [Table of Contents](#table-of-contents)
  - [Project Structure](#project-structure)
  - [Installation](#installation)
  - [Usage](#usage)
    - [Running the Simulation](#running-the-simulation)
    - [Using the Visualizer](#using-the-visualizer)
    - [Generating Plots](#generating-plots)
  - [Classes](#classes)
    - [Core Classes](#core-classes)
    - [Robot Types](#robot-types)


## Project Structure  
```
Robot_Simulation/
├── Robot_Simulation.py    # Main simulation logic and robot classes
├── Verify_Movement.py     # Script to run and visualize robot movement
├── Visualizer.py          # Visualization code using Tkinter
├── README.md              # This file
├── requirements.txt       # Project dependencies
└── .gitignore             # Files and directories to ignore
```
      

## Installation
1.  **Clone the repository:**

    ```bash
    git clone https://github.com/SherwinGPT/Robot-Simulation.git
    cd Robot_Simulation
    ```

2.  **Create and activate a virtual environment (highly recommended):**

    ```bash
    python3 -m venv .venv
    source .venv/bin/activate  # On Linux/macOS
    # OR
    .venv\Scripts\activate  # On Windows (cmd.exe)
    # .venv\Scripts\Activate.ps1  # On Windows (powershell)
    ```

3.  **Install dependencies:**

    ```bash
    pip install -r requirements.txt
    ```


## Usage
### Running the Simulation
The `run_simulation` function in `Robot_Simulation.py` is the primary way to run simulations.  Here's how to use it:

```python
import Robot_Simulation

# Example: Run a simulation with one StandardRobot in a 10x10 room
avg_time_steps = Robot_Simulation.run_simulation(
    num_robots=1,
    speed=1.0,
    capacity=1,
    width=10,
    height=10,
    dirt_amount=3,
    min_coverage=0.8,  # Clean 80% of the room
    num_trials=50,
    robot_type=Robot_Simulation.StandardRobot
)

print(f"Average time steps to clean 80% of the room: {avg_time_steps}")

# Example with a FaultyRobot
avg_time_steps_faulty = Robot_Simulation.run_simulation(
    num_robots=1,
    speed=1.0,
    capacity=1,
    width=10,
    height=10,
    dirt_amount=3,
    min_coverage=0.8,
    num_trials=50,
    robot_type=Robot_Simulation.FaultyRobot
)

print(f"Average time steps (FaultyRobot): {avg_time_steps_faulty}")
```

The script already includes example calls to run_simulation and prints the results. You can run the script directly:
      
```bash
python Robot_Simulation.py
```


### Using the Visualizer
The Visualizer is in the 'Verify_Movement.py' file. The test_robot_movement function from 'Verify_Movement.py' is 
already uncommented in 'Robot_Simulation.py' and will run automatically when running 'Robot_Simulation.py'. 
You can comment them out by searching with Ctrl+f for "Uncomment" to only generate the graphs.


### Generating Plots
The `Robot_Simulation.py` file contains two functions for generating plots:

*   `show_plot_compare_strategies(title, x_label, y_label)`: Compares the performance of StandardRobot and FaultyRobot based on the number of robots.

*   `show_plot_room_shape(title, x_label, y_label)`: Shows how cleaning time varies with different room aspect ratios.

These functions are already called at the end of `Robot_Simulation.py`. Run the script to generate and display the plots:
      
```bash
python Robot_Simulation.py
```


## Classes
### Core Classes
*   `Position(object)`: Represents a location (x, y) in the room.

*   `RectangularRoom(object)`: Base class for rooms. Manages tiles, dirt, and cleaning.

*   `EmptyRoom(RectangularRoom)`: A subclass of RectangularRoom with no obstacles.

*   `FurnishedRoom(RectangularRoom)`: A subclass of RectangularRoom with a single, randomly placed rectangular piece of furniture.

*   `Robot(object)`: Abstract base class for robots. Handles position, direction, speed, and cleaning capacity.


### Robot Types
*   `StandardRobot(Robot)`: Implements the standard movement strategy (move forward, change direction on collision).

*   `FaultyRobot(Robot)`: Implements a faulty movement strategy (probability of random direction change and failure to clean).