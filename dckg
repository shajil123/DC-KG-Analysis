from neo4j import GraphDatabase
import networkx as nx
from pyvis.network import Network
import webbrowser
import os

# --------- 1. Connect to Neo4j ---------
# Set your Neo4j credentials
NEO4J_URI = "Put the NEO4J URI here"
NEO4J_USER = "neo4j"
NEO4J_PASSWORD = "Password of the neo4j instance"  # 🔒 Replace this with your Neo4j password

# Connect to the database
driver = GraphDatabase.driver(NEO4J_URI, auth=(NEO4J_USER, NEO4J_PASSWORD))

# --------- 2. Query and Build Graph ---------
def fetch_graph(tx):
    query = """
    MATCH (a)-[r]->(b)
    RETURN a.name AS source, b.name AS target, type(r) AS relation
    """
    result = tx.run(query)
    edges = [(record["source"], record["target"], record["relation"]) for record in result]
    return edges


# Create a NetworkX directed graph
G = nx.DiGraph()

with driver.session() as session:
    edges = session.read_transaction(fetch_graph)
    for source, target, relation in edges:
        G.add_edge(source, target, label=relation)

driver.close()

# --------- 3. Visualize with Pyvis ---------
net = Network(height="750px", width="100%", bgcolor="#222222", font_color="white", notebook=False)

# Optional: Assign node colors
node_colors = ['#03dac6' for _ in G.nodes]

for idx, node in enumerate(G.nodes):
    net.add_node(node, label=node, color=node_colors[idx])

for edge in G.edges:
    label = G.edges[edge].get('label', '')
    net.add_edge(edge[0], edge[1], label=label)

# --------- 4. Save & Open HTML ---------
html_path = "knowledge_graph.html"
net.show(html_path)
webbrowser.open('file://' + os.path.realpath(html_path))

