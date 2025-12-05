Info on what notebook does what / how they are connected:

1. load_snRNA-seq-MDD.ipynb
Exploratory quality control for male and female datasets separately
Not used by any of the other notebooks

2. load_snRNA-seq-MDD-for-concatenated.ipynb
Uses the raw datasets from data/PRJNA602867 and data/PRJNA883411
Loads raw male and female objects and performs preprocessing (aka filtering of low-quality cells and genes) for joint integration
Outputs a combined AnnData object with male and female data, used by all downstream analyses
The "important" load notebook for our follow-up project

[NOTE Liv: markers = dc.get_resource("PanglaoDB") gives me an error]

3. joint_analysis_filtering_on_pv_neurons.ipynb
Uses the concatenated dataset (from 2. load_snRNA-seq-MDD-for-concatenated.ipynb) to:
- Score cell types (PanglaoDB) --> predict which cell type each cluster represents (NOTE: this part of the code doesn't run on my PC due to a decoupler error!)
- Identify inhibitory neurons and filter PVALB interneurons
- Export a clean PV-only dataset with complete metadata 
--> keep only the inhibitory neurons that express the PV-specific marker genes [PVALB, GAD1, GAD2] and remove all other cells from the dataset

4. ClusteringOfPVInterNeurons.ipynb
Uses the 3. joint_analysis_filtering_on_pv_neurons.ipynb notebook (more specific the generated PV dataset)
Branch for female-only PV interneuron re-clustering.
Mostly for comparisons I believe.

5. snRNA-esketamine-analysis.ipynb
Uses the 3. joint_analysis_filtering_on_pv_neurons.ipynb notebook (more specific the generated PV dataset)
Seems to include the main analysis:
- PV-specific reprocessing
- Re-clusters PV interneurons
- Conducts differential expression:
    -- MDD vs Ctrl
    -- Male vs Female
    -- Esketamine responder vs non-responder
- Generates main biological interpretations and figures