# ros2-gazebo-teleop-sim 🤖

ROS 2 + Gazebo simulation of a differential-drive bot designed in Fusion 360,
exported to URDF, and driven with keyboard teleop.

## Demo
<!-- Add a screenshot or GIF: put it in docs/ and use ![demo](docs/demo.gif) -->

## Environment
- Ubuntu 24.04 (WSL2)
- ROS 2 Jazzy
- Gazebo Harmonic (`gz sim`)

```bash
sudo apt install ros-jazzy-ros-gz ros-jazzy-teleop-twist-keyboard
```

## Repository structure
```
├── Fusion360_design/            # STEP files (base, wheels, assembly)
└── Simulation_Bot_description/
    ├── urdf/                    # Robot description (xacro)
    ├── meshes/                  # STL files
    ├── worlds/lfw.sdf           # Gazebo world used for teleop
    ├── launch/
    ├── package.xml
    └── CMakeLists.txt
```

## Run the teleop simulation
Clone the repo, then open three terminals. Run
`source /opt/ros/jazzy/setup.bash` in each one.

**Terminal 1: Gazebo**
```bash
cd ros2-gazebo-teleop-sim/Simulation_Bot_description
gz sim -r worlds/lfw.sdf
```

**Terminal 2: ROS–Gazebo bridge** (`/cmd_vel` from ROS to Gazebo)
```bash
ros2 run ros_gz_bridge parameter_bridge /cmd_vel@geometry_msgs/msg/Twist]gz.msgs.Twist
```

**Terminal 3: Teleop**
```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

Keys: `i` forward, `,` backward, `j` / `l` turn, `k` stop.
To slow the bot down, add `--ros-args -p speed:=0.15 -p turn:=0.8`.

## Design workflow
Fusion 360 → URDF export ([fusion2urdf](https://github.com/syuntoku14/fusion2urdf)) → Gazebo world → ROS 2 teleop.

## Notes
- The `.launch` files and `controller.yaml` from the exporter are ROS 1 format and are not used here.

## Author
Shubham, Electronics, Communication and Information Engineering, Tribhuvan University (IOE Purwanchal Campus)
