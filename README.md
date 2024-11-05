# Langgraph-and-Panel-App
### Panel App with Agents: Science Problem Creation, Translation, and LaTeX Generation
This notebook is organized into three key sections, detailed below, to guide you through creating science problems, translating them, and generating LaTeX files.


### Part 1: Workflow Creation with Math Agent
The Math Agent leverages LangGraph to generate a comprehensive workflow. In this process, a math problem is first created and then solved using the Wolfram tool, ensuring accurate and efficient problem-solving.

### Part 2: Math Creator Initialization and Execution
The Math Creator initializes and runs the Math Agent, providing a streamlined way to generate and solve problems. Optionally, the generated problem and solution can be translated and saved into a LaTeX file for professional formatting and presentation.

### Part 3: Integrated Panel in Math App
The Math App features an integrated panel that consolidates all essential tools and functions into a single, user-friendly interface, allowing users to seamlessly access and utilize all app features.

### utilities: 
Contains Latex formatting instructions.

Imports libraries and reads API keys from chatgpt_credentials.yml.

chatgpt_credentials.yml requires the following API keys:

openai_api_key: sk-proj ....

deepl_api_key: ...

wolfram_alpha_api_key: ...

# Math Agent: Automated Math Problem Generation and Solution Workflow

This repository provides the `Math_Agent` class, designed to automate the generation and solution of mathematical problems using a directed graph of nodes. Each node represents a step in the process, leveraging a language model (LLM) and external tools (e.g., WolframAlpha) for advanced computations. The agent is capable of creating problem statements and solving them, making it an ideal tool for educational and content creation purposes.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
  - [Components](#components)
  - [Example Workflow](#example-workflow)
- [License](#license)

---

## Overview

`Math_Agent` is a Python-based automation agent that uses a graph to orchestrate mathematical problem creation and solving. The process involves:

1. **Problem Generation**: Uses a specified expert domain and user-defined task to generate a math problem.
2. **Solution Node**: Solves the generated problem, optionally invoking external computational tools when needed.
3. **Tool Integration**: Integrates specialized tools, such as WolframAlpha, to handle complex computations beyond the scope of the language model.

---

## Features

- **Modular Workflow**: Step-by-step problem generation and solving within a structured, state-based graph.
- **Dynamic Task Definition**: Customizable problem generation based on specified expert domain and task application.
- **Tool Integration**: Incorporates external tools for enhanced computational support.
- **State Management**: Tracks the problem, messages, and responses at each node.

---

## Requirements

- Python 3.8+
- Required dependencies:
  ```bash
  pip install typing-extensions
  ```

Access to an LLM model API (e.g., GPT-3) and an external tool API (e.g., WolframAlpha) if used.

---

## Installation

1. Clone the repository.
2. Install the dependencies as listed in the [Requirements](#requirements) section.

---

## Usage

### Components

1. **Math_Agent Class**: Core agent for problem generation and solving.
   - **State**: Maintains details about the task, problem, messages, and more.
   
2. **Nodes**:
   - **create_node**: Generates a math problem based on expert and task input.
   - **solve_node**: Solves the problem, potentially involving external computational tools.
   
3. **Graph Initialization**:
   - **init_graph**: Initializes a directed graph with nodes and sets conditions for task execution flow.

### Example Workflow

1. **Initialize the Math Agent**:
   ```python
   math_agent = Math_Agent("gpt3")  # Specify the language model (e.g., GPT-3)
   graph = math_agent.init_graph()
   ```

2. **Define Task Details**:
   ```python
   state = Math_Agent.State(
       expert="Mathematics Expert",
       task="Create calculus problem",
       application="Education",
       problem="",
       messages=[]
   )
   ```

3. **Run the Graph**:
   ```python
   state = math_agent.run_graph(state, graph)
   print("Generated Problem:", state["problem"])
   print("Solution:", state["messages"][-1].content)
   ```

After running, `state["problem"]` contains the problem statement, while `state["messages"]` stores the solution steps or results.

`Math_Agent` provides a robust and scalable approach to creating and solving math problems programmatically. Its graph-based architecture and tool integration make it versatile for educational content creation and complex mathematical workflows.

# Math Creator: Automated Math Problem Generation, Formatting, and Translation

This repository contains the `Math_Creator` class, a powerful tool for generating, formatting, and translating math problems using a language model (LLM). `Math_Creator` allows users to specify a task and application area, then generates and solves the problem, optionally formatting the output in LaTeX or translating it to other languages. This tool is ideal for educators, students, and content creators in the field of mathematics.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
  - [Methods](#methods)
  - [Example Workflow](#example-workflow)
- [License](#license)

---

## Overview

`Math_Creator` builds on `Math_Agent` to offer a complete solution for generating math problems, formatting the output, and supporting multilingual translations. It includes features for:

1. **Problem Generation and Solution**: Automatically generates math problems based on user-defined expert level, task, and application context.
2. **LaTeX Formatting**: Optionally formats the generated problem and solution in LaTeX for display or publication.
3. **Translation Support**: Translates the solution into other languages, currently supporting German.

---

## Features

- **Dynamic Problem Creation**: Creates customized math problems based on provided task descriptions and applications.
- **LaTeX Output**: Formats solutions in LaTeX for academic publishing or educational resources.
- **Multilingual Translation**: Translates solutions into other languages, ideal for creating multilingual educational materials.
- **File Exporting**: Saves formatted outputs in `.tex` and `.html` formats.

---

## Requirements

- Python 3.8+
- Required dependencies:
  ```bash
  pip install typing-extensions panel
  ```

API access is required for the language model (e.g., GPT-3) and any translation services (e.g., DeepL API).

---

## Installation

1. Clone the repository.
2. Install dependencies as listed in [Requirements](#requirements).
3. Ensure that API keys are available for the LLM and translation service, if applicable.

---

## Usage

### Methods

1. **`init_agent(gpt_model)`**: Initializes a math problem-solving agent with the specified LLM model.

2. **`Run_Agent(expert, task, application)`**: Generates and solves a math problem based on the specified parameters.
   - `expert`: Domain expertise level (e.g., "Mathematics Expert").
   - `task`: Description of the task (e.g., "Matrices and determinants").
   - `application`: Real-world context (e.g., "apply to economics").
   
3. **`Latex(key)`**: Formats the solution in LaTeX if `key` is set to `"Yes"`, saving the result as a `.tex` file.

4. **`translate(key)`**: Translates the solution based on the `key` (e.g., `"German"`). If translated, saves a LaTeX version of the output as a `.tex` file.

5. **`Save_File(inp1, inp2, name)`**: Exports formatted content to `.tex` and `.html` files.

### Example Workflow

1. **Initialize Math_Creator**:
   ```python
   app = Math_Creator()
   app.init_agent("gpt3")  # Specify the LLM model
   ```

2. **Generate a Math Problem**:
   ```python
   output = app.Run_Agent("Mathematics Expert", "Create a calculus problem", "Education")
   print("Generated Problem and Solution:", output)
   ```

3. **Format in LaTeX**:
   ```python
   app.Latex("Yes")  # Save the output as a LaTeX file if desired
   ```

4. **Translate the Solution**:
   ```python
   translated_output = app.translate("German")
   print("Translated Output:", translated_output)
   ```

After running the workflow, LaTeX-formatted and translated files are saved in the `outputfiles` directory.


`Math_Creator` provides a comprehensive solution for generating, formatting, and translating mathematical problems, making it an essential tool for creating high-quality educational content. Its modular design supports easy customization and scalability.

# Math_APP: Interactive Math Problem Creation, Solution, and Formatting Application

`Math_APP` is a panel-based interactive application that allows users to generate, solve, format, and translate math problems. It utilizes `Math_Creator`, a class designed to interact with language models (e.g., GPT-3, GPT-4) to generate problems based on user inputs and context. The application provides a user-friendly interface for selecting tasks, formatting outputs in LaTeX, and translating solutions, making it suitable for educational content creation.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
  - [UI Components](#ui-components)
  - [Example Workflow](#example-workflow)
- [License](#license)

---

## Overview

`Math_APP` offers an intuitive user interface to interactively generate, solve, and format math problems. Users can define a mathematical task, specify its application, and receive a solution, which can then be formatted in LaTeX or translated into other languages (e.g., German). The application is built using the Panel library, with a range of widgets to control inputs and display outputs.

---

## Features

- **Task and Model Selection**: Customize the math task and choose from several language models (e.g., GPT-3, GPT-4).
- **Dynamic Problem Creation**: Generate tailored math problems based on the specified task and application area.
- **LaTeX Formatting**: Optionally format the output in LaTeX for easy use in documents.
- **Multilingual Translation**: Translate solutions into other languages to broaden accessibility.
- **Interactive UI**: Panel-based interface with widgets for task inputs, output display, and file export options.

---

## Requirements

- Python 3.8+
- Required dependencies:
  ```bash
  pip install panel
  ```

API access for the selected language model (e.g., OpenAI GPT API) and translation service (e.g., DeepL) if multilingual support is needed.

---

## Installation

1. Clone the repository.
2. Install dependencies as listed in [Requirements](#requirements).
3. Run the app script to launch the interface.

---

## Usage

### UI Components

1. **Model Selector (`self.gpt`)**: Choose from available language models like "gpt3" or "gpt4".

2. **Task Input (`self.task`)**: Input box for defining the mathematical task (e.g., "Matrices and determinants").

3. **Expert Level (`self.expert`)**: Choose the expertise level, such as "Math" or "Physics".

4. **Application Context (`self.application`)**: Input box for specifying the real-world context of the task (e.g., "apply to economics").

5. **Output Controls**:
   - **LaTeX Option (`self.Latex`)**: Select whether to create a LaTeX file of the solution.
   - **Language Selector (`self.language`)**: Choose a target language for translation (e.g., German).

6. **Buttons**:
   - **Start Button**: Triggers the generation of the math problem.
   - **Translation Button**: Translates the output into the selected language.
   - **LaTeX Button**: Formats the solution in LaTeX and saves the output.

### Example Workflow

1. **Initialize and Start the Application**:
   ```python
   app = Math_APP()
   Tabs = app.create_layout()
   layout = pn.Column(
       pn.Tabs(('HPS', Tabs[0]), ('Latex and Translation', Tabs[1]))
   )
   layout.show()
   ```

2. **Interact with the UI**:
   - **Select a Model**: Choose your preferred language model (e.g., "gpt4").
   - **Define Task and Application**: Enter a math task and specify a real-world application for context.
   - **Generate Problem**: Click the "Answer" button to generate and display the solution.
   - **Format in LaTeX**: Choose "Yes" for LaTeX output and click the "Latex" button to save it.
   - **Translate Solution**: Select a language (e.g., "German") and click "Translation" to view the translated solution.

3. **View Outputs**:
   - Generated problems and solutions are displayed under "Answer."
   - Translated content appears in the "Translation" pane.
   - LaTeX-formatted solutions are saved in the specified directory.

---


`Math_APP` provides a streamlined, interactive experience for creating and formatting math problems with flexible options for formatting and translation. This tool is ideal for creating engaging and accessible math content for educational purposes.
