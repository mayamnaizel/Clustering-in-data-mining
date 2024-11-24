# Step 1: Set Up the EC2 Ubuntu Instance
Launch an EC2 instance:
Update and install necessary packages:

sudo apt update && sudo apt upgrade -y
sudo apt install python3-pip -y

your EC2 Ubuntu environment is set up with a system-managed Python installation. This is typical for environments prioritizing stability, as the Python version is linked to the operating system's dependencies.

------------------------------------------------------------


# Step 2: Use a Virtual Environment
Install venv (if not already installed):

sudo apt update
sudo apt install python3-venv -y

Create a virtual environment:

python3 -m venv myenv

Activate the virtual environment:
source myenv/bin/activate

Install required packages within the virtual environment:

pip install pandas numpy scikit-learn matplotlib

Run your script while the virtual environment is active.

------------------------------------------------------------


# Step 3: Prepare the Dataset
Create a file data.csv:

nano data.csv

Paste the following content (simple 2D data for clustering):

X,Y
1,2
1.5,1.8
5,8
8,8
1,0.6
9,11
8,2
10,2
9,3

Save and exit (CTRL+O, CTRL+X).

------------------------------------------------------------


# Step 4: Implement K-Means Clustering
Create a Python script:

nano clustering.py

Paste the following code:

import pandas as pd
import numpy as np
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# Load the dataset
data = pd.read_csv("data.csv")

# Perform clustering
kmeans = KMeans(n_clusters=2, random_state=42)
kmeans.fit(data)

# Add cluster labels to the dataset
data['Cluster'] = kmeans.labels_

# Print results
print("Cluster Centers:")
print(kmeans.cluster_centers_)
print("\nClustered Data:")
print(data)

# Visualize the clusters
plt.scatter(data['X'], data['Y'], c=data['Cluster'], cmap='viridis', marker='o')
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], s=200, c='red', marker='x')
plt.title('K-Means Clustering')
plt.xlabel('X')
plt.ylabel('Y')
plt.show()

------------------------------------------------------------

# Step 5: Run the Script
Run the Python script:

python3 clustering.py


Expected Output
Cluster centers printed in the terminal.
A visualization of clusters displayed, with red "X" marking the cluster centers

------------------------------------------------------------


# Step 6: Analyze Results
Observe how the data points are grouped.
Experiment by changing n_clusters to 3 or more.

This lab demonstrates how clustering works with a simple dataset and enables you to experiment with clustering parameters and visualize results.
