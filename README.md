# QGISMCP4Ollama - QGIS Model Context Protocol Integration

QGISMCP4Ollama connects [QGIS](https://qgis.org/) to any Ollama-hosted LLM through the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/docs/getting-started/intro), allowing agentic interacations with and control of QGIS. This integration enables prompt assisted project creation, layer loading, code execution and more.

This project is strongly based on the [BlenderMCP](https://github.com/ahujasid/blender-mcp/tree/main) project by [Siddharth Ahuja](https://x.com/sidahuj) and [QGIS MCP](https://github.com/jjsantos01/qgis_mcp) by [Juan Santos Ochoa](https://github.com/jjsantos01)    


## Components

The system consists of two main components:

1. **[QGIS plugin](/qgis_mcp_plugin/)**: A QGIS plugin that creates a socket server within QGIS to receive and execute commands.
2. **[MCP Server](/src/qgis_mcp/qgis_mcp_server.py)**: A Python server that implements the Model Context Protocol and connects to the QGIS plugin.

## Installation

### Prerequisites

- QGIS 3.X (tested with 3.38)
- Ollama an model with support for agents (tested with ministral-3:latest)

For the MCP server Python environment: 

`pip install fastmcp ollama requests lupa`

### QGIS plugin

You need to copy the folder [qgis_mcp_plugin](/qgis_mcp_plugin/) and its content on your QGIS profile plugins folder.


## Usage

### Starting the connection in QGIS

1. In QGIS, go to `plugins` > `QGIS MCP` > `QGIS MCP`
    ![plugins menu](/assets/imgs/qgis-plugins-menu.png)
2. Click "Start Server"
    ![start server](/assets/imgs/qgis-mcp-start-server.png)
    Will launch on localhost:9876 by default.
3. Check the logs to see the connection status 
    ![alt text](/assets/imgs/qgis-log.png)

### Starting the QGIS_MCP server

`python src/qgis_mcp/qgis_mcp_server.py `

Will launch on localhost:9877/sse by default.

![alt text](/assets/imgs/fast-mcp.png)

#### Tools

- `ping` - Simple ping command to check server connectivity
- `get_qgis_info` - Get QGIS information about the current installation
- `load_project` - Load a QGIS project from the specified path
- `create_new_project` - Create a new project and save it
- `get_project_info` - Get current project information
- `add_vector_layer` - Add a vector layer to the project
- `add_raster_layer` - Add a raster layer to the project
- `get_layers` - Retrieve all layers in the current project
- `remove_layer` - Remove a layer from the project by its ID
- `zoom_to_layer` - Zoom to the extent of a specified layer
- `get_layer_features` - Retrieve features from a vector layer with an optional limit
- `execute_processing` - Execute a processing algorithm with the given parameters
- `save_project` - Save the current project to the given path
- `render_map` - Render the current map view to an image file
- `execute_code` - Execute arbitrary PyQGIS code provided as a string

### Starting the conversation

You can launch an example conversation using: 

`python src/qgis_mcp/qgis_mcp_client.py `

Note: you need to update the project file path to point to a project file on your machine. 

![alt text](/assets/imgs/convo.png)