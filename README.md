🛑 STOP
This is an implementation of the Agent Orchestration framework described in https://github.com/Platform-Studio/orchestra

It is implemented as a Python CLI that uses the local file system for persistence.

It's fine for local usage on your machine, but it might not be the best choice if you are working as part of a team or if you want to deploy it in a production environment.

The idea here is that you create your own implementation of the framework that fits your needs, from the specs.

# Prerequisites
- Python 3.x
- pip (Python package installer)
- CrewAI - https://github.com/crewaiinc/crewai
- Agent definitions in ./Agents

# Documentation
Documentation is in `./orchestration_cli.md`.

Point your agent of choice at this file.

# Example Agent Definition
Thre is an example agent definition in `./Agents/sorter.md`.

This agent looks for tasks in a workstream called `fruit_and_veg`, assesses whether each item is a fruit or a vegetable based on its title, and moves it to the corresponding state. 

If you want to run the commands yourself, versus having your agent call them, here's how to get it working:

1. Create a workstream:

```bash
python -m orchestration.cli workstream create --name "fruit_and_veg" --description "Workstream for sorting produce items into fruits and vegetables"
```

2. Add a Trigger that fires when a Task is added to the workstream:

```bash
python -m orchestration.cli trigger create WORKSTREAM_ID --on-state "pending" --action run_agent --agent sorter
```

3. Add some tasks:

```bash
python -m orchestration.cli task create WORKSTREAM_ID --title "Tomato" --description "A red, round produce item often used in salads and cooking."
python -m orchestration.cli task create WORKSTREAM_ID --title "Carrot" --description "An orange, crunchy vegetable commonly used in soups and salads."
python -m orchestration.cli task create WORKSTREAM_ID --title "Strawberry" --description "A sweet, red fruit with seeds on the outside, often used in desserts and smoothies."
```