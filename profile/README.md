# 🤖 AdaptiFleet: The Flexible, VLM-Powered Autonomous Fleet

> **Vision:** Bridging the "Human Intent Gap" to create fully autonomous warehouses and robot fleets capable of delivering on-demand fulfillment in any environment—from logistics to healthcare and beyond.

[![AdaptiFleet Presentation](https://img.shields.io/badge/Presentation-Lablab.ai-blue?style=for-the-badge)](https://lablab.ai/ai-hackathons/launch-fund-ai-meets-robotics/adaptifleet/adaptifleet)

## 🌟 The Mission
Traditional warehouse automation is rigid and hard to reconfigure. **AdaptiFleet** solves this by using a single, adaptable AI brain—powered by **Google Gemini 3 Pro VLMs**—to manage a fleet of robots. Non-technical users can deploy complex automation using natural language commands, enabling **10x faster deployment** and **95% reduction in downtime**.

## Gemini

### Gemini 3 Usage

We use **Google Gemini 3** (`gemini-3-flash`) in our pipeline for two purposes:

[Repository](https://github.com/rueabk/robotics-isaacsim)

| Where | File | Use |
|-------|------|-----|
| **LLM prompt API** | `llm_prompt_api.py` | Parses natural language prompts (e.g. *"move robot 2 to reception"*) and extracts structured robot movement tasks (robot + waypoint). Handles synonyms, multiple tasks, and legacy location names. Powers the `/prompt` API for fleet control. |
| **Scene guard VLM** | `scene_guard_vlm.py` | Analyzes robot camera feeds in real time. Detects fallen parcels and obstacles blocking the path. Publishes safety events on `/safety/events` to halt or alert when hazards are detected. |

### Gemini Robotics ER-1.5 Usage

[Repository](https://github.com/rueabk/robotics_backend)

We leverage Google Gemini Robotics ER-1.5 as the planner of our operation.

#### Core Endpoints

`api/v1/plan` (Mission Orchestration):

Acts as the high-level dispatcher. It processes complex, multi-step goals (e.g., "Coordinate a delivery from shelf A to the drone station using Carter") and generates a logical sequence of robot actions. It maps user intent to the LLM Prompt API to handle task decomposition.

`api/v1/execute` (Spatial Grounding):

Acts as the precision controller. It uses Vision-Language Modeling (VLM) to analyze specific camera frames. It returns 0-1000 normalized coordinates for bounding boxes and grasp points, allowing robots to interact with objects they have never seen before.


## 🏗️ Technical Architecture
Our modular "Digital Twin Stack" ensures simulation-validated intent meets real-world execution across our five core modules:

1. **[Dashboard](https://github.com/om3gaholdings/nowww3/)** - The tactical "Mission Control" center for live robot tracking and map overlays.
2. **[Gemini robotics backend](https://github.com/rueabk/robotics_backend)** - The Gemini-powered reasoning engine for semantic hazard detection and task planning.
3. **[Robotics Sim in IsaacSim](https://github.com/rueabk/robotics-isaacsim)** - High-fidelity physics simulation for rapid validation of warehouse and office behaviors.
4. **[ROS2 Bridge WS](https://github.com/rueabk/robotics-isaacsim/tree/main/ros_ws/src)** - The communication layer transforming simulated world data for the frontend.
5. **[AI Order Backend](https://github.com/AdaptiFleet/ai-backend)** - Inventory management and customer-to-operator notification bridge.

## 🚀 Future Roadmap
AdaptiFleet scales beyond logistics into **Healthcare** (medication delivery), **Defense** (unpredictable environment logistics), **Corporate Offices**, and **Entertainment**.

---
*Developed for the Lablab.ai Launch & Fund Hackathon.*
