# ![CI logo](https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png)

# Membrane Protein Structural Data Analysis

## Project Overview

Membrane proteins are proteins that interact with or are embedded in biological membranes. Biological membranes form boundaries around cells and many structures inside cells. They separate different environments while allowing cells to communicate, transport substances, produce energy, and respond to signals.

Membrane proteins are therefore involved in many essential biological processes. Examples include receptors that allow cells to respond to hormones or other signals, channels that allow ions to cross membranes, transporters that move molecules into and out of cells, and proteins involved in energy production.

They are also particularly important in medicine because many therapeutic drugs act on membrane proteins.

Studying membrane proteins experimentally can be challenging because their interaction with membranes makes them more difficult to isolate and characterise than many soluble proteins. Structural databases provide an opportunity to examine large numbers of experimentally studied membrane proteins and identify broader patterns in their structural properties.

This project performs an exploratory data analysis of membrane protein structural data obtained from the OPM (Orientations of Proteins in Membranes) database.

The analysis investigates:

- which membrane environments and protein families are most represented;
- how structural properties differ between membrane environments;
- whether structural complexity is associated with structural resolution;
- and which structural properties show meaningful relationships with each other.

Python, Pandas, Matplotlib and Seaborn are used to clean, explore, analyse and visualise the data.

## Understanding the Biological Context

No previous knowledge of membrane protein biology is required to understand this project. The main concepts used in the analysis are explained below.

### Biological Membranes

A biological membrane can be thought of as a thin boundary separating one biological environment from another.

The plasma membrane, for example, surrounds a cell and separates the inside of the cell from its external environment. Cells also contain internal membranes surrounding structures such as mitochondria, the endoplasmic reticulum and lysosomes.

Different organisms also have different membrane systems. For example, Gram-negative bacteria contain both inner and outer membranes.

### Membrane Proteins

Membrane proteins are proteins associated with biological membranes. Some pass completely through a membrane, while others interact only with its surface.

A protein can cross a membrane once or many times. Proteins containing many membrane-spanning segments can form large and structurally complex membrane protein systems.

### Membrane Environment

In this project, `membrane_name_cache` describes the membrane environment associated with each structure.

Examples include:

- eukaryotic plasma membrane;
- Gram-negative bacterial inner membrane;
- Gram-negative bacterial outer membrane;
- mitochondrial inner membrane;
- endoplasmic reticulum;
- thylakoid membrane;
- viral membranes;
- and secreted proteins.

These categories allow structural properties to be compared between different biological environments.

### Protein Families

Proteins with related structures or functions can be grouped into protein families.

For example, G-protein coupled receptors (GPCRs) form a large family of membrane proteins involved in cellular signalling.

Analysing protein families helps identify which types of proteins are particularly well represented in the structural dataset.

### Membrane Thickness

Membrane thickness describes the estimated thickness of the membrane region associated with a protein structure.

Comparing thickness across membrane environments can reveal whether proteins associated with different types of membranes occupy structurally different membrane regions.

### Protein Tilt

Tilt describes the orientation of a protein relative to the membrane.

A low tilt value indicates a different orientation relative to the membrane than a high tilt value. Comparing tilt distributions can therefore reveal differences in how proteins are positioned within or relative to membranes.

### Membrane-Spanning Segments

`subunit_segments` represents the number of membrane-spanning segments associated with a structure.

In this project, this variable is used as an approximate indicator of structural complexity. A protein or protein complex containing many membrane-spanning segments is generally structurally more complex than one containing only a few.

### Structural Resolution

Structural resolution describes the level of structural detail available for an experimentally determined protein structure and is commonly reported in Ångströms (Å).

An Ångström is a very small unit of length equal to 0.1 nanometres.

Importantly:

**A smaller numerical resolution value generally represents finer structural detail, while a larger value represents lower structural detail.**

For example, a structure determined at 2 Å generally contains finer structural information than one determined at 5 Å.

### Gibbs Free Energy

The dataset also contains a Gibbs free-energy variable (`gibbs`).

In this project, Gibbs free energy is treated as a numerical structural property supplied by the source dataset. Relationships between this variable and other structural properties are explored statistically without assuming that correlation represents a causal biological mechanism.


## Project Objectives

The overall objective of this project is to explore a large membrane protein structural dataset and identify understandable patterns in its composition and structural properties.

The specific objectives are to:

- clean and prepare the original dataset for reliable analysis;
- identify the most represented membrane environments;
- identify the most represented protein families;
- compare structural properties across different membrane environments;
- investigate whether structural complexity is associated with structural resolution;
- identify relationships between numerical structural properties;
- visualise the findings clearly;
- and communicate the results in a way that can be understood without specialist knowledge of structural biology.

## Research Questions

The exploratory analysis addresses four research questions:

1. **Which membrane environments and protein families are most represented in the dataset?**

2. **How do structural properties such as membrane thickness, protein tilt and structural resolution differ between membrane environments?**

3. **Is structural complexity, represented by the number of membrane-spanning segments, associated with structural resolution?**

4. **Which numerical structural properties show meaningful relationships with each other?**

## Dataset

The project uses structural membrane protein data obtained from the **OPM (Orientations of Proteins in Membranes) database**.

OPM provides information about experimentally determined protein structures and their relationships with biological membranes.

The original dataset contains thousands of structural records and includes biological, structural and database-related information.

Some of the most important variables used in this project are:

| Variable | Description |
|---|---|
| `pdbid` | Identifier linking the structure to the Protein Data Bank (PDB) |
| `name` | Name or description of the protein structure |
| `family_name_cache` | Protein family classification |
| `species_name_cache` | Organism associated with the structure |
| `membrane_name_cache` | Membrane environment associated with the structure |
| `thickness` | Estimated membrane thickness |
| `tilt` | Protein orientation/tilt relative to the membrane |
| `subunit_segments` | Number of membrane-spanning segments |
| `gibbs` | Gibbs free-energy value supplied by the dataset |
| `resolution` | Original structural resolution information |
| `resolution_numeric` | Cleaned numerical representation of structural resolution |
| `uniprotcode` | UniProt identifier where available |

### Dataset Size

After data cleaning, the dataset used for analysis contains **8,914 records and 29 variables**.

Not every variable is used in the exploratory analysis. Variables were selected according to their relevance to the four research questions.

## Data Cleaning and Preparation

Before exploratory analysis, the dataset was examined for formatting problems, missing information, duplicate records and potentially unusual numerical values.

The cleaning process was designed to preserve valid scientific information rather than automatically removing unusual observations.

### PDB Identifiers

PDB identifiers contained formatting introduced by the original data export. These identifiers were cleaned into a consistent format so that structures could be identified reliably.

### Structural Resolution

The original `resolution` variable contained both numerical and non-numerical information.

A separate `resolution_numeric` variable was therefore created for analyses requiring numerical resolution values.

Where a numerical resolution was unavailable, the value was retained as missing rather than artificially estimated.

### Missing Values

Missing values were examined individually according to the meaning of each variable.

Values were not automatically replaced with averages or other estimated values when there was insufficient evidence to justify imputation.

For example, missing values in `topology_subunit` were investigated in relation to the number of membrane-spanning segments. The majority of records with missing topology information had zero membrane-spanning segments, but exceptions were also present. Missing topology values were therefore retained rather than replaced with an assumed category.

Missing values in uncertainty-related variables such as `thicknesserror` and `tilterror` were also retained when no reliable replacement could be justified.

### Duplicate Records

Potential duplicate PDB identifiers were investigated rather than immediately deleted.

Where apparently duplicated structures contained differences in database metadata or represented separate records, they were retained to avoid removing potentially valid information without sufficient evidence.

### Text Formatting

Leading and trailing whitespace was identified in categorical text fields such as protein family and species names and removed to prevent identical categories from being treated as different values.

### Numerical Validation

Important numerical variables were checked for impossible or unusual values.

The analysis included checks for:

- negative membrane thickness;
- negative protein tilt;
- tilt values above 90 degrees;
- negative membrane-spanning segment counts;
- and unusually large uncertainty values.

Extreme values were inspected rather than automatically removed. Where there was no evidence that an observation represented a data-entry error, it was retained.

### Cleaning Principle

The overall cleaning strategy followed a conservative principle:

> **Unusual scientific observations should not be removed simply because they are statistical outliers.**

This is particularly important for biological structural data, where unusual structures may represent genuine and scientifically interesting observations.

## Exploratory Data Analysis

The cleaned dataset was explored using descriptive statistics and visualisation.

The analysis used:

- frequency counts for categorical variables;
- summary statistics including means and medians;
- bar charts to examine category representation;
- violin plots to examine structural-property distributions;
- scatter plots to examine relationships between numerical variables;
- Pearson correlation to examine linear relationships;
- Spearman correlation to examine monotonic relationships;
- and correlation heatmaps to summarise relationships between structural properties.

Both Pearson and Spearman correlations were considered because several variables contain skewed distributions and extreme values.

Pearson correlation measures the strength of a linear relationship between two numerical variables.

Spearman correlation is based on ranked values and can identify monotonic relationships even when the relationship is not strongly linear. It is also less sensitive to extreme values.

Correlation coefficients range from -1 to +1:

- values close to +1 indicate a strong positive association;
- values close to -1 indicate a strong negative association;
- values close to 0 indicate little or no monotonic or linear association, depending on the correlation method used.

Correlation does not demonstrate that one variable causes another.

## Key Findings

### 1. Which membrane environments and protein families are most represented?

The dataset is not evenly distributed across membrane environments.

The largest membrane-environment category is **eukaryotic plasma membrane**, containing 3,316 records. Other strongly represented categories include secreted proteins and Gram-negative bacterial inner-membrane proteins.

Some membrane environments contain only a small number of structures.

This means that the dataset should not be interpreted as showing how common different membrane proteins are in nature. Instead, it reflects the structures represented in the OPM dataset.

The protein-family distribution is also highly uneven.

The most represented family is **G-protein coupled receptors, family A**, with 664 records. Other strongly represented families include transient receptor potential channels, V-type and F-type ATPases, NADH dehydrogenases and glutamate-gated ion channels.

This concentration is biologically interesting because several highly represented families are important signalling, transport or energy-conversion proteins. However, their frequency in this dataset represents structural database coverage rather than their biological abundance.

### 2. How do structural properties differ between membrane environments?

Clear differences were observed in membrane thickness and protein tilt between membrane environments.

Most major transmembrane environments have median membrane thickness values approximately between 24 and 31 Å.

Eukaryotic plasma membrane proteins have a median thickness of approximately 31 Å, while thylakoid, Gram-positive inner-membrane and Gram-negative inner-membrane proteins also have median values close to 30 Å.

Secreted and Undefined structures show much lower thickness values than the main transmembrane categories.

A violin plot was used to visualise membrane thickness because several categories contain complex distributions. Unlike a simple boxplot, the violin plot makes it easier to see where observations are concentrated within each group.

Protein tilt also differs substantially between membrane environments.

Most major membrane categories have relatively low median tilt values, whereas the Secreted and Undefined categories contain substantially higher values.

Structural resolution varies less dramatically between membrane environments than thickness or tilt.

Among records with numerical resolution information, median resolution values for the major categories are generally around 2–3 Å.

These findings indicate that structural properties are associated with membrane environment, although they do not demonstrate that membrane environment directly causes these differences.

### 3. Is structural complexity associated with structural resolution?

The number of membrane-spanning segments was used as an approximate indicator of structural complexity.

Among the 7,575 records containing both membrane-spanning segment information and numerical structural resolution, the distributions were strongly skewed.

Seventy-five percent of these structures contain 24 or fewer membrane-spanning segments, while a small number of highly complex structures contain substantially more, reaching a maximum of 389 segments.

Two correlation approaches were used:

- **Pearson correlation: 0.197**
- **Spearman correlation: 0.445**

The Pearson result indicates a weak positive linear relationship.

The stronger Spearman result indicates a moderate positive monotonic relationship. In other words, structures containing more membrane-spanning segments generally tend to have higher numerical resolution values, although the relationship is not strongly linear.

Because a higher resolution value in Å corresponds to lower structural detail, the result suggests that structurally more complex membrane proteins tend, on average, to be resolved at somewhat lower structural detail.

This relationship should be interpreted as an association rather than evidence that structural complexity directly causes lower structural resolution.

### 4. Which structural properties are related?

The correlation analysis identified several strong relationships between numerical structural properties.

The strongest Spearman relationship was observed between the number of membrane-spanning segments and Gibbs free energy:

**Spearman ρ = -0.925**

This represents a very strong negative monotonic association.

Protein tilt also shows strong relationships with structural complexity and Gibbs free energy:

- tilt vs membrane-spanning segments: **ρ = -0.813**
- tilt vs Gibbs free energy: **ρ = 0.807**

Membrane thickness is also associated with several structural variables:

- thickness vs membrane-spanning segments: **ρ = 0.590**
- thickness vs tilt: **ρ = -0.634**
- thickness vs Gibbs free energy: **ρ = -0.694**

Structural resolution shows more moderate relationships with the other structural variables.

The Spearman correlations were generally stronger than the corresponding Pearson correlations for several variable pairs. This suggests that some relationships in the dataset are monotonic but not strongly linear.

Again, these correlations identify statistical relationships. They do not establish biological causation.

## Conclusions

The project demonstrates that a large structural membrane-protein dataset can reveal clear patterns in both database composition and structural characteristics.

The main conclusions are:

1. **The dataset is highly unevenly represented.**  
Eukaryotic plasma membrane proteins and several major protein families, particularly family A GPCRs, account for substantial proportions of the available structures.

2. **Membrane environment is associated with structural differences.**  
Membrane thickness and protein tilt differ substantially between membrane environments, while structural resolution shows smaller differences.

3. **Structural complexity is associated with structural resolution.**  
The number of membrane-spanning segments shows a moderate monotonic association with numerical structural resolution.

4. **Structural properties are interconnected.**  
Strong relationships exist between membrane-spanning segment count, Gibbs free energy, protein tilt and membrane thickness.

The project therefore shows that membrane protein structures cannot be considered as a single homogeneous group. Their structural characteristics vary according to biological context and are related to other measurable structural properties.

At the same time, the analysis is exploratory. The observed relationships describe patterns within the dataset and should not be interpreted as demonstrating causal biological mechanisms.

## Limitations

Several limitations should be considered when interpreting this project.

### Unequal Group Sizes

Membrane environments and protein families contain very different numbers of structures.

A category containing thousands of structures provides much more information than one containing only a few records. Direct comparisons should therefore be interpreted carefully.

### Database Representation Is Not Biological Abundance

A protein family being common in the dataset does not necessarily mean that it is equally common in living organisms.

Structural databases are influenced by scientific interest, experimental feasibility and the availability of experimentally determined structures.

### Missing Resolution Information

Not every structure has a numerical resolution value.

Records without suitable numerical resolution information were excluded only from analyses that specifically required numerical resolution. Missing values were not artificially imputed.

### Extreme Values

Several numerical variables contain extreme observations.

These values were retained when there was no evidence that they represented errors. Biological structural datasets can contain genuinely unusual structures, so statistical outliers should not automatically be treated as invalid observations.

### Structural Complexity

The number of membrane-spanning segments was used as an approximate measure of structural complexity.

Real protein structural complexity is more complicated and can also depend on factors such as protein size, number of subunits, domain organisation and interactions with other molecules.

### Correlation Is Not Causation

The project identifies associations between structural variables.

For example, finding that structures with more membrane-spanning segments tend to have different resolution values does not prove that the number of segments directly causes the difference in resolution.

Other biological and experimental factors may contribute to the observed relationships.

## Repository Structure

The project is organised into separate folders for data and analysis notebooks.

```text
membrane-protein-data-analysis/
│
├── data/
│   └── proteins_cleaned.csv
│
├── jupyter_notebooks/
│   ├── 01_data_cleaning.ipynb
│   └── 02_data_analysis.ipynb
│
├── .gitignore
├── README.md
└── requirements.txt
```


## Technologies Used

### Python

Python is the main programming language used for data preparation and analysis.

### Pandas

Pandas is used for:

- loading tabular data;
- cleaning and transforming variables;
- handling missing values;
- grouping observations;
- calculating descriptive statistics;
- and preparing data for visualisation.

### NumPy

NumPy supports numerical operations used during data preparation and analysis.

### Matplotlib

Matplotlib is used to create and customise data visualisations.

### Seaborn

Seaborn is used for statistical visualisations including violin plots, scatter plots and correlation heatmaps.

### Jupyter Notebook

Jupyter notebooks are used to combine executable Python code, analytical results, visualisations and written interpretation in a reproducible workflow.

### Git and GitHub

Git is used for version control and GitHub is used to store and document the project repository.


### AI-Assisted Development

AI tools were used selectively during the development of this project as a supporting resource.

AI assistance was mainly used for:

- clarifying Python and Pandas syntax when needed;
- troubleshooting errors during notebook development;
- suggesting approaches for data visualisation and presentation;
- improving the clarity and structure of Markdown documentation;
- and reviewing explanations for readability.

The data-cleaning decisions, selection of research questions, interpretation of the dataset, and final analytical decisions were reviewed and implemented by the project author. AI-generated suggestions were not treated as results and were checked against the actual dataset before being included in the project.

## How to Run the Project

To run the project locally:

1. Clone the GitHub repository to your computer.
2. Open the project folder in VS Code or another compatible development environment.
3. Create and activate a Python virtual environment.
4. Install the required Python packages using:

```bash
pip install -r requirements.txt
```

## Development Notes

Git and GitHub were used for version control throughout the project. During the early stages of development, several changes were grouped into larger commits rather than committed individually. As the project progressed, a more granular approach to version control was adopted, with smaller and more descriptive commits used to document individual changes and improvements.

## Future Work

This project focuses on exploratory structural analysis. Several extensions could provide additional biological and therapeutic context.

Potential future work includes:

- linking structures to additional UniProt functional annotations;
- incorporating disease associations;
- identifying known therapeutic or drug targets;
- integrating ligand and drug-binding information;
- comparing experimental methods with achievable structural resolution;
- investigating individual membrane-protein families in greater detail;
- and examining whether structural characteristics differ between therapeutic targets and other membrane proteins.

One particularly interesting extension would be to connect the structural dataset with disease and drug-target databases. This could help investigate whether proteins of therapeutic interest occupy particular membrane environments or share structural characteristics.

These extensions are outside the current project's scope but provide clear directions for further analysis.

## Data Source and Credits

### Dataset

The dataset used in this project was obtained from the **OPM (Orientations of Proteins in Membranes) database**, maintained by the University of Michigan.

OPM provides structural information about proteins associated with biological membranes, including their positioning and orientation relative to the membrane.

For this project, the **proteins dataset** was downloaded from the OPM download page:

[OPM Database - Download Data](https://opm.phar.umich.edu/download)

The original dataset was subsequently cleaned and prepared for analysis within this project. All analyses, transformations and visualisations presented in the project were performed on the downloaded OPM data.

### Project Template

The initial repository structure was based on the **Code Institute Data Analytics project template**.

The template provided the basic project structure and configuration files used to begin the project. The original template README instructions were replaced with documentation specific to this membrane protein data analysis project.

Code Institute Data Analytics template:

[Code Institute Data Analytics Template](https://github.com/Code-Institute-Org/data-analytics-template)

### Acknowledgements

This project was completed as part of the **Code Institute Data Analytics with AI programme**.

Guidance provided during the course was used to improve the organisation, documentation, version-control practices and presentation of the project.

AI tools were used selectively as a supporting resource during development, as described in the Technologies Used section. Analytical decisions and final interpretations were reviewed against the actual dataset before inclusion in the project.

