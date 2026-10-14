AI-Based Autonomous Mobile Robot Navigation System
An autonomous mobile robot navigation simulation built with Python and a browser-based dashboard. The project combines global path planning, local obstacle avoidance, robot motion control, 3D visualization, and automated benchmarking.
Features
Robot models: TurtleBot3 Burger, Waffle, and Pioneer configurations.
Global path planning: A*, RRT*, and Genetic Algorithm (GA), with a safe A* fallback where supported.
Local planning and obstacle avoidance: Artificial Potential Field (APF), ANFIS-adapted APF, and Dynamic Window Approach (DWA).
Motion controllers: Computed-Torque Control (CTC), Adaptive Computed-Torque Control, and Sliding Mode Control (SMC).
Interactive web dashboard: Run and configure simulations in a browser.
2D and 3D views: View the map, planned path, robot trajectory, and moving obstacles.
Start/goal selection: Choose start and goal positions in the dashboard.
Benchmarking: Compare navigation performance using success rate, path length, smoothness, convergence time, computation time, and torque-work energy.
Dynamics verification and tests: Includes symbolic dynamics verification and automated self-tests.
Project Structure
```text
robotics project 2/
├── main.py
├── run_3d.py
├── requirements.txt
├── config/
│   └── robot_configs.py
├── controllers/
│   ├── computed_torque.py
│   ├── adaptive_fuzzy.py
│   ├── sliding_mode.py
│   └── lyapunov_kinematic.py
├── planners/
│   ├── global_planners.py
│   ├── local_planners.py
│   └── intelligent_adaptation.py
├── robot_model/
│   ├── dynamics.py
│   ├── kinematics.py
│   └── symbolic_verifier.py
├── simulation/
│   ├── simulator.py
│   └── benchmark.py
├── tests/
├── web/
│   ├── app.py
│   ├── templates/
│   └── static/
└── README.md
```
Requirements
Python 3.10 or a compatible Python version
pip
A modern web browser
Python packages are listed in `requirements.txt`, including Flask, NumPy, SymPy, and Matplotlib.
Installation
Clone or download this repository.
Open a terminal in the project directory (the directory containing `main.py`).
Install the dependencies:
```bash
   python -m pip install -r requirements.txt
   ```
Run the Web Dashboard
Start the application:
```bash
python main.py --port 5050
```
Then open this URL in your browser:
```text
http://localhost:5050
```
Use the dashboard to configure the robot, planner, local obstacle-avoidance method, controller, and simulation start/goal. The default port is `5050`.
Run the 3D Python Viewer
The project also includes a standalone Python 3D visualization:
```bash
python run_3d.py
```
Example with custom settings:
```bash
python run_3d.py --robot waffle --planner RRTStar --local DWA --controller SMC
```
Choose custom start and goal coordinates:
```bash
python run_3d.py --start 1 9 --goal 9 1 --seed 3
```
Save an animation or final image without opening the viewer:
```bash
python run_3d.py --save demo.gif --no-show
python run_3d.py --png final.png --no-show
```
The standalone 3D viewer uses Matplotlib.
Testing and Verification
Run the project self-test:
```bash
python main.py --self-test
```
Run the test modules directly:
```bash
python -m unittest tests.test_full_execution tests.test_system
```
Verify the symbolic robot dynamics:
```bash
python main.py --verify
```
It compares the symbolic formulations used for the Lagrangian and Newton–Euler dynamics.
Run Benchmarks
Run the benchmark suite from the command line:
```bash
python main.py --benchmark
```
The benchmark suite evaluates navigation performance over multiple trials. Results include success rate, mean path length, smoothness, convergence time, computation time per step, and torque-work energy.
Recommended Starting Configuration
Robot: TurtleBot3 Burger
Global planner: A*
Local planner: ANFIS-adapted APF
Controller: Adaptive Computed-Torque Control
Speed: 0.50 m/s
You can change these options in the dashboard to compare behavior across configurations.
How It Works
The simulation creates a map containing static and dynamic obstacles.
A global planner calculates a collision-free route from the start to the goal.
A local planner chooses movement commands while responding to nearby obstacles.
The controller converts the desired motion into control inputs for the robot model.
The simulation updates the robot and obstacle states and checks for collisions or goal completion.
The dashboard visualizes the robot, route, trajectory, and obstacles. Benchmark mode aggregates performance metrics.
Notes
Run commands from the project root—the folder containing `main.py`.
If you change the source code and encounter issues, run `python main.py --self-test` to check the system.
If port `5050` is already in use, choose another port, for example `python main.py --port 5051`, and open `http://localhost:5051`.
The standalone Python 3D viewer requires Matplotlib. The browser dashboard has its own 3D renderer.
Future Improvements
Test planning and control methods across more map layouts and obstacle patterns.
Add exportable benchmark reports and plots.
Extend the robot models and controller tuning options.
Evaluate performance on physical robot hardware.
License
No license file was included with the supplied project archive. Add a `LICENSE` file before publishing if you want to specify how others may use, modify, and distribute this project.
