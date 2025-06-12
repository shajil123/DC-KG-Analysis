# Neo4j Graph Visualizer

A Python tool for visualizing Neo4j graph databases using interactive web-based visualization. This tool connects to your Neo4j database, extracts graph data, and creates an interactive HTML visualization that opens in your web browser.

## Features

- 🔗 **Direct Neo4j Integration**: Connects directly to your Neo4j database instance
- 🎨 **Interactive Visualization**: Creates interactive graph visualizations using Pyvis
- 🌐 **Web-Based Output**: Generates HTML files that can be viewed in any web browser
- 🎯 **Customizable Styling**: Dark theme with customizable node colors and layouts
- 📊 **Relationship Mapping**: Displays both nodes and their relationships with labels

## Prerequisites

Before running this tool, make sure you have:

- Python 3.7 or higher
- A running Neo4j database instance
- Neo4j connection credentials (URI, username, password)

## Installation

1. **Clone or download the script**
   ```bash
   git clone <repository-url>
   cd neo4j-graph-visualizer
   ```

2. **Install required dependencies**
   ```bash
   pip install neo4j networkx pyvis
   ```

## Configuration

Before running the script, you need to configure your Neo4j connection settings:

1. Open `neo4jGraphVisualizer.py`
2. Update the following variables with your Neo4j instance details:

```python
NEO4J_URI = "bolt://localhost:7687"  # Your Neo4j URI
NEO4J_USER = "neo4j"                 # Your username
NEO4J_PASSWORD = "your_password"     # Your password
```

### Common Neo4j URI formats:
- Local instance: `bolt://localhost:7687`
- Neo4j Aura: `neo4j+s://your-instance.databases.neo4j.io`
- Remote instance: `bolt://your-server:7687`

## Usage

1. **Ensure your Neo4j database is running**

2. **Run the visualizer**
   ```bash
   python neo4jGraphVisualizer.py
   ```

3. **View the results**
   - The script will generate `knowledge_graph.html` in the same directory
   - Your default web browser will automatically open the visualization
   - If it doesn't open automatically, manually open the HTML file

## How It Works

The script performs the following steps:

1. **Database Connection**: Establishes a connection to your Neo4j database
2. **Data Extraction**: Runs a Cypher query to fetch all nodes and relationships
3. **Graph Building**: Creates a NetworkX directed graph from the extracted data
4. **Visualization**: Uses Pyvis to create an interactive HTML visualization
5. **Display**: Opens the visualization in your web browser

## Customization

### Modifying the Query

The default query extracts all relationships:
```cypher
MATCH (a)-[r]->(b)
RETURN a.name AS source, b.name AS target, type(r) AS relation
```

You can customize this query to:
- Filter specific node types: `MATCH (a:Person)-[r]->(b:Company)`
- Limit results: `MATCH (a)-[r]->(b) RETURN a.name AS source, b.name AS target, type(r) AS relation LIMIT 100`
- Add node properties: Include additional node attributes in the RETURN clause

### Styling Options

You can customize the visualization appearance:

```python
# Network appearance
net = Network(
    height="750px",        # Visualization height
    width="100%",          # Visualization width
    bgcolor="#222222",     # Background color
    font_color="white",    # Text color
    notebook=False
)

# Node colors
node_colors = ['#03dac6', '#ff6b6b', '#4ecdc4']  # Add multiple colors
```

### Advanced Configuration

For more advanced styling, you can:
- Set different colors for different node types
- Adjust physics simulation parameters
- Modify edge styling and thickness
- Add custom node sizes based on properties

## Troubleshooting

### Common Issues

1. **Connection Error**
   ```
   ServiceUnavailable: Could not connect to Neo4j
   ```
   - Verify your Neo4j instance is running
   - Check your URI, username, and password
   - Ensure the Neo4j service is accessible from your network

2. **Authentication Error**
   ```
   AuthError: The client is unauthorized
   ```
   - Verify your username and password
   - Check if your Neo4j user has read permissions

3. **Empty Graph**
   - Ensure your database contains data
   - Verify nodes have a `name` property
   - Check if your query returns results in Neo4j Browser

4. **HTML File Not Opening**
   - Check if the HTML file was created in the script directory
   - Manually open `knowledge_graph.html` in your browser
   - Verify your system's default browser is set correctly

### Query Debugging

To debug your query, test it first in Neo4j Browser:
```cypher
MATCH (a)-[r]->(b)
RETURN a.name AS source, b.name AS target, type(r) AS relation
LIMIT 10
```

## Dependencies

- **neo4j**: Neo4j Python driver for database connectivity
- **networkx**: Graph data structure and analysis library
- **pyvis**: Interactive network visualization library

## File Structure

```
neo4j-graph-visualizer/
├── neo4jGraphVisualizer.py    # Main script
├── knowledge_graph.html       # Generated visualization (after running)
└── README.md                  # This file
```

## Contributing

Feel free to contribute improvements:
- Add support for different node properties
- Implement clustering algorithms
- Add export options for different formats
- Improve error handling and logging

## License

This project is open source. Please check the repository for license details.

## Support

For issues related to:
- **Neo4j**: Check the [Neo4j Documentation](https://neo4j.com/docs/)
- **Pyvis**: Visit the [Pyvis Documentation](https://pyvis.readthedocs.io/)
- **NetworkX**: See the [NetworkX Documentation](https://networkx.org/documentation/)

---

**Note**: Always ensure your Neo4j credentials are kept secure and never commit them to version control systems.
