# CLAUDE.md - executive_smach_visualization

## Overview

Third-party ROS 2 metapackage for SMACH state machine visualization. Originally maintained by Jonathan Bohren, now orphaned. Used in the MAIRON project to visualize Flexbotics process execution.

## Structure

```plaintext
executive_smach_visualization/
├── executive_smach_visualization/   # Metapackage (ament_cmake)
│   ├── package.xml
│   └── CMakeLists.txt
└── smach_viewer/                    # Main package (ament_cmake + Python)
    ├── package.xml
    ├── CMakeLists.txt
    ├── scripts/
    │   └── smach_viewer.py          # Main GUI app (~1096 lines, wxPython)
    └── smach_viewer_module/
        ├── __init__.py
        ├── wxxdot.py                # wxPython xdot widget (Cairo rendering)
        └── xdot_qt.py               # PyQt4/PyQt5 xdot widget (alternative)
```

## Build

```bash
colcon build --packages-select smach_viewer executive_smach_visualization
```

## Key Classes (smach_viewer.py)

- **ContainerNode**: Represents a SMACH container, generates DOT code, tracks active/initial states
- **SmachViewerFrame**: Main wxPython frame with graph view, tree view, and userdata panel
- **MyApp**: Minimal wx.App subclass

## ROS 2 Interface

- **Node:** `smach_viewer`
- **Subscribes:** `<server>/smach/container_structures` (`SmachContainerStructure`), `<server>/smach/container_status` (`SmachContainerStatus`)
- **Service client:** `<server>/smach/set_initial_state`
- **Discovery:** Uses `smach_ros.IntrospectionClient()` to find SMACH servers dynamically

## Dual GUI Backend

- `wxxdot.py` — wxPython + Cairo (primary, used by smach_viewer.py)
- `xdot_qt.py` — PyQt4/PyQt5 (alternative, 2234 lines, standalone xdot implementation)

## Notes

- No launch files, no tests, no config files
- Travis CI badge in old README references melodic-devel (outdated)
- pytest setup is commented out in CMakeLists.txt
- This is an external dependency — avoid heavy modifications
