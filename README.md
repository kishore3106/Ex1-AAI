<H3>Name : KISHORE B</H3>

<H3>Register No. : 212224100032</H3>

<H3>Experiment 1</H3>

<H3>DATE : 20.07.2026</H3>

<H1 ALIGN=CENTER>Implementation of Bayesian Networks</H1>

## Aim
To create a Bayesian Network for the given weather dataset using Python.

## Algorithm

**Step 1:** Import necessary libraries such as `pandas`, `networkx`, `matplotlib.pyplot`, and the required `pybbn` modules.

**Step 2:** Set pandas display options to show more columns.

**Step 3:** Read the weather dataset from the CSV file.

**Step 4:** Remove records where the target variable `RainTomorrow` contains missing values.

**Step 5:** Fill missing values in the remaining numerical columns using the column mean.

**Step 6:** Create categorical bands (`HumidityBand` and `TempBand`) from the selected weather attributes.

**Step 7:** Display a snapshot of the processed dataset.

**Step 8:** Define a function to calculate probability distributions for the Bayesian Belief Network.

**Step 9:** Create `BbnNode` objects for `HumidityBand`, `TempBand`, and `RainTomorrow` using the calculated probabilities.

**Step 10:** Create the Bayesian Network by adding nodes and directed edges.

**Step 11:** Convert the Bayesian Network into a Join Tree using the `InferenceController`.

**Step 12:** Specify the positions of the nodes for visualization.

**Step 13:** Configure the graph appearance and generate the Bayesian Network graph.

**Step 14:** Display the generated Bayesian Network graph.


## Program

```python
# Install (run once)
# pip install pybbn

import pandas as pd
import networkx as nx
import matplotlib.pyplot as plt

from pybbn.graph.dag import Bbn
from pybbn.graph.edge import Edge, EdgeType
from pybbn.graph.node import BbnNode
from pybbn.graph.variable import Variable
from pybbn.pptc.inferencecontroller import InferenceController

# Load dataset
df = pd.read_csv("weatherAUS.csv")

# Data preprocessing
df = df.dropna(subset=["RainTomorrow"])
df = df.fillna(df.mean(numeric_only=True))

# Create bands
df["HumidityBand"] = pd.cut(
    df["Humidity3pm"],
    bins=[0, 30, 60, 100],
    labels=["Low", "Medium", "High"]
)

df["TempBand"] = pd.cut(
    df["Temp3pm"],
    bins=[-10, 20, 30, 50],
    labels=["Low", "Medium", "High"]
)

# Function to calculate probabilities
def get_probs(data, child, parents=[]):
    if len(parents) == 0:
        return data[child].value_counts(normalize=True).sort_index().values.tolist()

    elif len(parents) == 1:
        return pd.crosstab(
            data[parents[0]],
            data[child],
            normalize="index"
        ).sort_index().values.flatten().tolist()

    elif len(parents) == 2:
        return pd.crosstab(
            [data[parents[0]], data[parents[1]]],
            data[child],
            normalize="index"
        ).sort_index().values.flatten().tolist()

# Create nodes
humidity = BbnNode(
    Variable(0, "HumidityBand", ["Low", "Medium", "High"]),
    get_probs(df, "HumidityBand")
)

temp = BbnNode(
    Variable(1, "TempBand", ["Low", "Medium", "High"]),
    get_probs(df, "TempBand")
)

rain = BbnNode(
    Variable(2, "RainTomorrow", ["No", "Yes"]),
    get_probs(df, "RainTomorrow", ["HumidityBand", "TempBand"])
)

# Build Bayesian Network
bbn = Bbn()
bbn.add_node(humidity)
bbn.add_node(temp)
bbn.add_node(rain)

bbn.add_edge(Edge(humidity, rain, EdgeType.DIRECTED))
bbn.add_edge(Edge(temp, rain, EdgeType.DIRECTED))

# Perform inference
join_tree = InferenceController.apply(bbn)

# Draw graph
G = nx.DiGraph()
G.add_edge("HumidityBand", "RainTomorrow")
G.add_edge("TempBand", "RainTomorrow")

pos = {
    "HumidityBand": (0, 1),
    "TempBand": (2, 1),
    "RainTomorrow": (1, 0)
}

plt.figure(figsize=(8, 5))
nx.draw_networkx(
    G,
    pos,
    node_color="skyblue",
    node_size=3500,
    with_labels=True,
    font_size=11,
    font_weight="bold",
    arrows=True,
    arrowsize=25
)

plt.title("Bayesian Belief Network")
plt.axis("off")
plt.show()
````


## Output

* Dataset after preprocessing (`df.head()`)

  <img width="1492" height="468" alt="image" src="https://github.com/user-attachments/assets/279de127-e02f-4f17-99b6-3d5af2af6dea" />
  

* Generated Bayesian Network graph

<img width="885" height="592" alt="image" src="https://github.com/user-attachments/assets/af275a2e-ab3b-41ef-bc21-4de1b2736993" />



## Result

Thus, a Bayesian Network was successfully implemented and visualized using Python for the given weather dataset.

