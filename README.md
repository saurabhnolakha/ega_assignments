# ASCII Exponential Calculator with Paint Visualization

## Overview

This project demonstrates an advanced use of Multi-modal Cognitive Programming (MCP) to perform mathematical operations and visualize results using macOS's Paintbrush application. The system uses Gemini AI to orchestrate tool calls, performing a chain of operations:

1. Convert text to ASCII values
2. Calculate exponential sums of those values
3. Visualize the result by drawing a rectangle in Paintbrush and adding text

## Project Structure

The project consists of two main files:

- `talk2mcp-2_modified.py` - Main orchestration script that handles LLM interactions and function call parsing
- `mcp_tools.py` - Tool definitions for mathematical operations and UI automation

## Prerequisites

- Python 3.8+
- macOS with Paintbrush application installed
- Gemini API key

## Required Packages

```
pip install python-dotenv mcp google-generativeai pyautogui rich
```

## Configuration

Create a `.env` file in the project root with your Gemini API key:

```
GEMINI_API_KEY=your_key_here
```

## How It Works

### Main Flow (talk2mcp-2_modified.py)

The `talk2mcp-2_modified.py` script:

1. Establishes an MCP server connection to `mcp_tools.py`
2. Loads available tools through the MCP interface
3. Creates a system prompt that instructs the LLM how to use the tools
4. Presents a specific task to the LLM: "Find the ASCII values of characters in INDIA and then return sum of exponentials of those values. Open paint, draw a rectangle And print the result inside a rectangle in paint."
5. Processes LLM responses in an iteration loop (up to 5 iterations):
   - Parses JSON-formatted function calls using regex and JSON validation
   - Executes the corresponding tools through the MCP interface
   - Provides feedback to the LLM for the next iteration

The script includes robust functions for validating and correcting JSON, handling improperly formatted responses from the LLM.

### Available Tools (mcp_tools.py)

The `mcp_tools.py` script defines all the tools that can be called by the LLM:

#### ASCII and Exponential Operations
- `strings_to_chars_to_int`: Converts text characters to ASCII values
- `int_list_to_exponential_sum`: Calculates sum of exponentials of a list of integers

#### Paint Operations
- `open_paint`: Opens Paintbrush application
- `draw_rectangle`: Draws a rectangle in the Paintbrush window
- `add_text_in_paint`: Adds text inside the rectangle

#### Mathematical Operations
- Basic arithmetic: `add`, `subtract`, `multiply`, `divide`
- Advanced math: `power`, `sqrt`, `log`, `factorial`
- Trigonometric functions: `sin`, `cos`, `tan`

## Example Usage

Run the main script:

```
python talk2mcp-2_modified.py
```

This will orchestrate the following workflow:
1. The LLM analyzes the task and calls `strings_to_chars_to_int` with "INDIA" as input
2. It takes the resulting ASCII values and calls `int_list_to_exponential_sum` to calculate the sum
3. It calls `open_paint` to launch the Paintbrush application
4. It calls `draw_rectangle` to create a rectangle in the canvas
5. It calls `add_text_in_paint` to display the result inside the rectangle

## Troubleshooting

- **JSON Parsing Errors**: The system includes robust error handling for malformed JSON from the LLM.
- **UI Automation Issues**: The code uses both AppleScript and PyAutoGUI as fallbacks for UI interactions.

## Extensions

This framework can be extended with additional tools by:
1. Adding new tool functions to `mcp_tools.py`
2. Updating the system prompt in `talk2mcp-2_modified.py` to include descriptions of the new tools 