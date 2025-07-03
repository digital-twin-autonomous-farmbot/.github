
This GitHub organization contains the complete ecosystem of repositories developed for autonomous agricultural robotics research, centered around the Project Work 2: **"Digital Twin for Autonomous Robots using ROS2"** and the Bachelor Thesis: **"Autonomous Robot for Plant Management and Energy Efficiency on Photovoltaic Green Rooftops"** at ZHAW (Zurich University of Applied Sciences).

## Project Overview

The organization encompasses a comprehensive digital twin system for autonomous agricultural robots, combining computer vision, robotics, and cloud technologies to enable automated plant monitoring and management on photovoltaic green rooftops.

## Repository Structure & Connections

### Core Digital Twin System

#### [`digital_twin`](./digital_twin)
**Main digital twin of the Project Work 2 implementation and experimental frameworks**
- **`model/`**: Complete batmobile robot digital twin with URDF models, Gazebo simulation, and RViz visualization
- **`robogardener/`**: Experimental package attempting to integrate Nav2, SLAM Toolbox, and ros2_control throughout the thesis(discontinued due to time constraints)
- **`nodes/`**: Supporting ROS2 nodes for experimental system extensions
- **Technologies**: ROS2 Jazzy, Gazebo, RViz2, URDF/XACRO
- **Status**: model: Operational - Used in PW2,  robogardener: experimental features incomplete

#### [`digital_twin_plants`](./digital_twin_plants)
**Plant analysis and monitoring pipeline**
- Computer vision-based plant species identification using Plant.id API
- Stereo camera depth calculation for plant height measurement
- Statistical analysis and correlation studies using R
- MongoDB integration for data storage and retrieval
- **Key Features**: Camera calibration, depth calculation, plant identification, statistical analysis
- **Technologies**: Python, OpenCV, Plant.id API, MongoDB, R
- **Status**: Production ready - Used in thesis

#### [`minibot`](./minibot) 
**Physical robot hardware configuration**
- Customized digital twin for differential drive robot
- RPLidar integration for SLAM and autonomous navigation
- Modified robot description matching physical hardware specifications
- **Hardware**: Differential drive platform, RPLidar sensor, custom actuators
- **Technologies**: ROS2 Jazzy, Navigation2, SLAM Toolbox
- **Status**: Operational - Used in thesis


### Hardware Integration Layer

#### [`ros_arduino_bridge`](./ros_arduino_bridge)
**Low-level motor control interface**
- Modified Arduino firmware for single-drive motor with steering control
- Serial communication bridge between ROS2 and Arduino hardware
- PWM signal generation for motors and servo control
- **Hardware**: Arduino, L298 motor driver, encoders, steering servo
- **Technologies**: Arduino C++, Serial communication, PWM control
- **Status**: Functional - Hardware abstraction layer

#### [`gopigo3_ros`](./gopigo3_ros)
**Alternative robot platform (experimental)**
- ROS2 package for GoPiGo3 robot control via Twist messages
- **Note**: Test implementation that failed due to OS/hardware compatibility issues
- **Technologies**: ROS2, Python, easygopigo3 library
- **Status**: Discontinued - Compatibility issues

### Deployment & Infrastructure

#### [`docker_container_robogardener`](./docker_container_robogardener)
**Containerized deployment system**
- **`raspberry_pi/`**: **Production deployment** - Camera services and image API for Raspberry Pi
  - Flask camera server for remote image capture
  - MongoDB-integrated image API
  - Used extensively in bachelor thesis
- **`test_images/ros2_jazzy_foxglove/`**: ROS2 Jazzy desktop with Foxglove visualization
- **`test_images/minibot/`**: Containerized minibot applications (build issues with expired GPG keys)
- **Technologies**: Docker, Docker Compose, Flask, MongoDB, Foxglove, Traefik
- **Status**: Raspberry Pi components production-ready, others experimental

## System Architecture & Data Flow

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────────┐
│   Physical      │    │   Digital Twin   │    │    Analysis &       │
│   Hardware      │◄──►│   Simulation     │◄──►│   Monitoring        │
│                 │    │                  │    │                     │
│ • minibot       │    │ • minibot        │    │ • digital_twin_     │
│ • ros_arduino_  │    │ • Gazebo sim     │    │   plants            │
│   bridge        │    │ • RViz viz       │    │ • Plant ID API      │
│ • RPLidar       │    │                  │    │ • Depth analysis    │
└─────────────────┘    └──────────────────┘    └─────────────────────┘
         │                       │                        │
         │               ┌────────────────┐               │
         └──────────────►│  Deployment    │◄──────────────┘
                         │  Infrastructure│
                         │                │
                         │ • docker_      │
                         │   container_   │
                         │   robogardener │
                         │ • Raspberry Pi │
                         │ • MongoDB      │
                         └────────────────┘
```

## Academic Context

This work represents the culmination of research conducted at **ZHAW (Zurich University of Applied Sciences)** focusing on:

- **Digital Twin Technology** for autonomous robots
- **Sustainable Agriculture** automation
- **Computer Vision** for plant monitoring
- **ROS2 Integration** for robotic systems
- **Energy Efficiency** on photovoltaic installations



## Getting Started

### Prerequisites
- **ROS2 Jazzy Jalisco** on Ubuntu 24.04
- **Docker & Docker Compose** for containerized deployment
- **Python 3.x** with OpenCV for computer vision components
- **Arduino IDE** for hardware programming
- **MongoDB** for data storage (optional, fallback to local files available)

### Quick Start
```bash
# Clone the organization repositories
git clone https://github.com/your-org/digital_twin.git
git clone https://github.com/your-org/digital_twin_plants.git
git clone https://github.com/your-org/minibot.git
# ... etc

# Start with the digital twin simulation
cd digital_twin/model
ros2 launch model model_motor.launch.py

# Deploy the Raspberry Pi services
cd docker_container_robogardener/raspberry_pi
docker-compose up -d

# Run plant analysis pipeline
cd digital_twin_plants
python main_measurement.py
```

## 📊 Repository Status Overview

| Repository | Status | Purpose | Technologies |
|------------|---------|---------|--------------|
| `digital_twin` | ✅ Core complete, ⚠️ Experimental incomplete | ROS2, Gazebo, URDF |
| `digital_twin_plants` | ✅ Production ready | Plant monitoring pipeline | Python, OpenCV, MongoDB |
| `minibot` | ✅ Operational | Physical robot platform | ROS2, Navigation2, RPLidar |
| `ros_arduino_bridge` | ✅ Functional | Hardware abstraction | Arduino, Serial, PWM |
| `gopigo3_ros` | ❌ Discontinued | Alternative platform | ROS2, Python |
| `docker_container_robogardener` | ✅ Pi ready, ⚠️ Others experimental | Deployment infrastructure | Docker, Flask, MongoDB |

## Author

**Noirin Graham** (grahanoi@students.zhaw.ch)  
Bachelor's Thesis, ZHAW - Zurich University of Applied Sciences

## License

Apache-2.0 License - See individual repositories for specific licensing information.


*This ecosystem represents a comprehensive approach to autonomous agricultural robotics, combining cutting-edge digital twin technology with practical plant monitoring solutions for sustainable farming applications.*
