<H3>Name : Logesh.N.A</H3>

<H3>Register No. : 212223240078</H3>

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
# Paste your complete Python program here
````


## Output

* Dataset after preprocessing (`df.head()`)

  <img width="1492" height="468" alt="image" src="https://github.com/user-attachments/assets/279de127-e02f-4f17-99b6-3d5af2af6dea" />
  

* Generated Bayesian Network graph

<img width="885" height="592" alt="image" src="https://github.com/user-attachments/assets/af275a2e-ab3b-41ef-bc21-4de1b2736993" />



## Result

Thus, a Bayesian Network was successfully implemented and visualized using Python for the given weather dataset.

