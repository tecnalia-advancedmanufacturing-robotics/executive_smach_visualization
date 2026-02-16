# executive_smach_visualization

GUI tools for visualizing and introspecting hierarchical SMACH state machines at runtime in ROS 2.

## Packages

| Package | Description |
|---|---|
| `executive_smach_visualization` | Metapackage |
| `smach_viewer` | wxPython GUI for real-time state machine visualization |

## Usage

```bash
# Launch the viewer
ros2 run smach_viewer smach_viewer.py

# With auto-focus on active states
ros2 run smach_viewer smach_viewer.py -f
```

The viewer automatically discovers running SMACH introspection servers and subscribes to their structure and status topics.

## Features

- Real-time visualization of active states, transitions, and hierarchy
- Adjustable depth for nested/compound state machines
- User data inspection panel for selected states
- Toggle implicit/explicit transitions
- Auto-focus mode to track active subgraph
- Tree view of state machine hierarchy
- Set initial states interactively

## Dependencies

- **ROS 2:** `rclpy`, `smach_ros`, `smach_msgs`, `cv_bridge`
- **GUI:** `python3-wxgtk4.0`, `python3-qt5-bindings`, `gtk3`
- **Graph:** `graphviz`, `python3-xdot`
- **Python:** `python3-gi`, `python3-gi-cairo`, `python3-rospkg`

## ROS 2 Interface

- **Node:** `smach_viewer`
- **Subscribes:** `<server>/smach/container_structures`, `<server>/smach/container_status`
- **Calls:** `<server>/smach/set_initial_state`

## License

BSD
