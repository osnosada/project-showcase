# Memory-Augmented VLM-Driven Tabletop Arrangement Robot

A simulation system where a **Panda robotic arm** understands **open-vocabulary natural language commands** via **Qwen2.5-VL** and performs multi-step pick-and-place operations in the **ManiSkill3** simulation environment.

**Demo Video:** [demo_video.mp4](./demo_video.mp4)

---

## System Architecture

```
Natural Language Command (e.g., "Put the fruit in the bowl")
        │
        ▼
┌─────────────────────────────────────┐
│    VLM Scene Understanding          │
│    (Qwen2.5-VL-3B/7B)              │
│    Image + Command → Structured JSON│
└─────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────┐
│    3-Level JSON Parsing Fallback    │
│    Direct → Clean Markdown → Regex  │
└─────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────┐
│    Memory & State Tracker           │
│    Prevents duplicate grasps &       │
│    incorrect operations              │
└─────────────────────────────────────┘
        │
        ▼
┌─────────────────────────────────────┐
│    Robot Action Executor             │
│    Motion Planning (mplib/RRT)      │
│    or Numerical Jacobian IK (fallback)│
└─────────────────────────────────────┘
        │
        ▼
    ManiSkill3 Simulation
    (Panda Robotic Arm)
```

---

## Key Features

| Feature | Description |
|---------|-------------|
| **Open-Vocabulary Commands** | Understands arbitrary natural language instructions (e.g., "Clean up the trash", "Put the fruit in the bowl") |
| **VLM Scene Understanding** | Qwen2.5-VL processes RGB images + commands to generate structured task lists |
| **3-Level Parsing Fallback** | Robust JSON extraction: direct parse → markdown cleanup → regex extraction → default task list |
| **Memory-Augmented Execution** | State tracking prevents duplicate grasps and incorrect operations |
| **Dual Execution Modes** | Motion planning (mplib + RRTConnect) or numerical Jacobian IK (auto-fallback) |
| **Semantic Name Mapping** | 50+ semantic name mappings supporting bilingual (Chinese/English) object references |
| **Dual Rendering** | GPU rendering (ManiSkill) or matplotlib fallback (compatible with all environments) |

---

## Tech Stack

| Category | Technology |
|----------|-----------|
| **Simulation** | ManiSkill3, SAPIEN |
| **VLM** | Qwen2.5-VL-3B/7B-Instruct (HuggingFace Transformers) |
| **Motion Planning** | mplib (RRTConnect/Screw), Numerical Jacobian IK |
| **Robot** | Panda robotic arm (7-DOF) |
| **Visualization** | matplotlib 3D, ManiSkill GPU renderer |
| **Language** | Python 3.10+ |

---

## My Contributions

As the **VLM interface core developer**, I was responsible for the critical bridge between language understanding and robot execution:

- **VLM Integration:** Integrated Qwen2.5-VL-3B/7B models, configured HuggingFace Chinese mirror for accelerated model downloads, implemented flash-attention-2 optional acceleration detection
- **3-Level JSON Parsing Fallback:** Built a robust parsing pipeline — direct JSON parse → markdown code block cleanup → regex-based extraction → default task list — ensuring the system never crashes on malformed VLM output
- **Semantic Name Mapping:** Constructed a comprehensive semantic mapping dictionary supporting 50+ object names in both Chinese and English, enabling the VLM's open-vocabulary output to map to simulation environment objects
- **Prompt Engineering:** Iterated 50+ prompt variations to optimize VLM output consistency, designed custom system prompts that enumerate scene objects and enforce structured JSON output
- **Bilingual Regex Parser:** Developed Chinese/English regex parsers for extracting structured data from VLM responses, validated across 20+ natural language instructions

---

## How It Works

### 1. Scene Understanding
The VLM receives a scene image and natural language command, outputting a structured task list:
```json
{
  "objects": [
    {"category": "fruit", "id": "cubeA_1", "target": "cubeB"}
  ]
}
```

### 2. Semantic Mapping
VLM semantic output maps to physical simulation objects:

| VLM Output | Simulation Object | Semantic Meaning |
|-----------|-------------------|-----------------|
| apple/fruit | Red sphere | Fruit item |
| bowl/container | Green bowl | Container |

### 3. Memory Tracking
The memory module tracks each object's state to prevent errors:
- `on_table` → `grasping` → `in_container`

### 4. Action Execution
Two execution modes (auto-detected):
- **Motion Planning** (requires mplib): PandaArmMotionPlanningSolver + RRTConnect
- **Numerical IK** (fallback): pd_joint_pos control + numerical Jacobian IK

---

## Demo Commands

```bash
# Quick test without VLM (uses fallback task list)
python test_e2e.py

# Run demo with 3 preset commands (requires VLM model)
python main.py --demo

# Single command
python main.py "Put the fruit in the bowl"

# Use larger VLM model
python main.py --model Qwen/Qwen2.5-VL-7B-Instruct --demo
```

---

## Results

- Pick-and-place success rate: **>90%** (numerical IK mode)
- Supports arbitrary open-vocabulary natural language commands
- 3-level parsing fallback ensures zero crashes from malformed VLM output
- Validated across 20+ natural language instructions
- 13+ dedicated test scripts with cross-version compatibility testing
- Successfully executes complex multi-step operations: "Take the carrot out of the bowl and put the eggplant inside"

---

## Team

| Member | Role |
|--------|------|
| **Li Yuanping** | VLM Interface and JSON Parsing Engine |
| Cheng Yazheng | Custom Environment and Simulation Core |
| Chen Zhishen | Scene Memory System |
| Yuan Jinjiang | Robot Motion Execution Support |
| Zhao Miyang | Pipeline Integration and Documentation |

---

*This project was developed for CS461 Robotics coursework at Macau University of Science and Technology.*
