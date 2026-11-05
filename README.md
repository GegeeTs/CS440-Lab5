# CS440 Lab 5: Q-learning with Isolate

CS440 - Artificial Intelligence
Colorado State University
Fall 2026

## Overview

This repository builds on Isolate to solve the vacuum robot problem with Q-learning. Lab 5 will use subagents, hooks, and skills in Claude Code.

A main agent splits the work and gives each part to a specialist. Each specialist receives only the context needed for its task and returns a short summary.

## Problem Description

The vacuum robot operates in a 4x4 grid.

| start | 0  | 0 | 0  |
|-------|----|---|----|
| 0     | X  | 0 | 0  |
| 0     | 0  | 0 | 0  |
| 0     | -1 | 0 | 10 |

The robot will use Q-learning without receiving explicit T and R tables.

Movement is 80% in the chosen direction and 10% in each perpendicular direction. Both -1 and +10 end an episode.

The current files contain the project context and subagent definitions. The Q-learning implementation, hooks, and skills still need to be added.

## Project Structure

```text
CS440-Lab5/
├── CLAUDE.md
├── README.md
├── q_learning.ipynb
├── requirements.txt
├── aima/
├── context/
│   ├── environment.md
│   └── requirements.md
└── .claude/
    └── agents/
        ├── environment-specialist.md
        ├── requirements-specialist.md
        └── configuration-reviewer.md
```

## File Descriptions

### q_learning.ipynb

Contains the trimmed Lab 3 environment and policy display, with TODOs for Q-learning, evaluation, and updated reward handling. It is not a working Lab 5 solution yet. The course AIMA package is included in `aima/`.

### aima/

Contains the unmodified course AIMA Python package from [carsonloedel/CS440](https://github.com/carsonloedel/CS440/tree/master/aima). Its license and exact source revision are recorded inside the folder.

### requirements.txt

Lists the dependencies for the notebook's AIMA import and Python kernel.

### CLAUDE.md

Contains the main instructions, specialist assignments, and delegation rules.

### context/environment.md

Documents the vacuum robot's grid, important locations, movement, and rewards.

### context/requirements.md

Documents the Lab 5 scope, proposed hyperparameters, and submission requirements.

### .claude/agents/environment-specialist.md

Defines the specialist that checks the grid and identifies unknown environment details.

### .claude/agents/requirements-specialist.md

Defines the specialist that checks the assignment scope and submission requirements.

### .claude/agents/configuration-reviewer.md

Defines the specialist that reviews selected configuration files for errors and contradictions.

## How the Strategy Works

1. You give Claude Code a task.
2. Claude reads CLAUDE.md and selects the appropriate specialists.
3. Each specialist receives a focused task and the relevant sources, rather than the full chat history.
4. Each specialist returns a short summary.
5. The main agent combines the findings into an answer.

All three specialists are read-only.

## Notebook Setup

From the CS440-Lab5 directory, install the notebook dependencies:

```sh
python -m pip install -r requirements.txt
```

Open `q_learning.ipynb` in VS Code and select that Python environment as the notebook kernel. The local `aima/` folder supplies `aima.agents`; `bootstrap.ipynb` is not needed for this import.

The notebook is still a starter. Its Q-learning, evaluation, recharge lookup, and reward-handling TODOs must be completed before a full run.

## Demonstration

1. Open a terminal in the CS440-Lab5 directory and start Claude Code.
2. Run `/agents` to check that the three specialists appear.
3. Ask Claude to review the grid and assignment requirements using the specialists.
4. Check the actual delegations and compare their responses with the source files.

## Expected Behavior

Claude should:

- Identify the start at (0, 0), obstacle, and reward cells correctly.
- Keep explicit T and R tables separate from the learning agent.
- Use Q-learning for the Lab 5 implementation.
- Give each specialist only the context needed for its task.
- Report missing information instead of inventing rules.

## Why This Is Context Engineering

The Isolate strategy separates tasks into focused contexts. This reduces irrelevant information and helps each specialist stay on its assigned task.

## Limitations

Training and evaluation commands will be documented when the implementation is added.

File boundaries are instructions, not enforced access restrictions. Responses and actual delegation should still be verified. A live Claude Code demonstration has not yet been tested.
