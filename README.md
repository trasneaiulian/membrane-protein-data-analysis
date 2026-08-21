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


## Template Instructions

Welcome,

This is the Code Institute student template for the three Data Analytics capstone projects. We have preinstalled all of the tools you need to get started. It's perfectly okay to use this template as the basis for your project submissions. Click the `Use this template` button above to get started.

You can safely delete the Template Instructions section of this README.md file and modify the remaining paragraphs for your own project. Please do read the Template Instructions at least once, though! It contains some important information about the IDE and the extensions we use.

If you are working on the first capstone project, you can also delete `.python-version`, `.slugignore`, `Procfile` and `setup.sh` as they are only required for later dashboard projects. 

## How to use this repo

1. Use this template to create your GitHub project repo. Click the **Use this template** button, then click **Create a new repository**.

1. Copy the URL of your repository to your clipboard.

1. In VS Code, select **File** -> **Open Folder**.

1. Select your `vscode-projects` folder, then click the **Select Folder** button on Windows, or the **Open** button on Mac.

1. From the top menu in VS Code, select **Terminal** > **New Terminal** to open a new terminal.

1. In the terminal, type `git clone` followed by the URL of your GitHub repository. Then hit **Enter**. This command will download all the files in your GitHub repository into your vscode-projects folder.

1. In VS Code, select **File** > **Open Folder** again.

1. This time, navigate to and select the folder for the project you just downloaded. Then, click **Select Folder**.

1. A virtual environment is necessary when working with Python projects to ensure each project's dependencies are kept separate. You need to create your virtual environment, also called a venv, and then activate it whenever you return to your workspace.
Click the gear icon in the lower left-hand corner of the screen to open the Manage menu and select **Command Palette** to open the VS Code command palette.

1. In the command palette, type: *create environment* and select **Python: Create Environment…**

1. Choose **Venv** from the dropdown list.

1. Choose the Python version you installed earlier. Currently, we recommend Python 3.12.8

1. **DO NOT** click the box next to `requirements.txt`; you need to complete additional steps before installing your dependencies. Click **OK**.

1. You will see a `.venv` folder appear in the file explorer pane, indicating that the virtual environment has been created.

1. **Important**: Note that the `.venv` folder is in the `.gitignore` file so that Git won't track it.

1. Return to the terminal by clicking on the TERMINAL tab, or click on the **Terminal** menu and choose **New Terminal** if no terminal is currently open.

1. In the terminal, use the command below to install your dependencies. This may take several minutes.

 ```console
 pip3 install -r requirements.txt
 ```

1. Open the `jupyter_notebooks` directory, and click on the notebook you want to open.

1. Click the **Kernel** button, then choose **Python Environments**.

Note that the kernel says `Python 3.12.8` as it inherits from the venv, so it will be Python-3.12.8 if that is what is installed on your PC. To confirm this, you can use the command below in a notebook code cell.

```console
! python --version
```

## Deployment Reminders

* The `.python-version`, `.slugignore`, `Procfile` and `setup.sh` files are necessary only if you are deploying a Streamlit app to Heroku as part of your submission for units 2 and 3. 
* Set the `.python-version` Python version to a [Heroku-22](https://devcenter.heroku.com/articles/python-support#supported-runtimes) stack, currently supported version that most closely matches what you used in this project.
* The project can be deployed to Heroku using the following steps.

1. Log in to Heroku and create an App
2. At the **Deploy** tab, select **GitHub** as the deployment method.
3. Select your repository name and click **Search**. Once it is found, click **Connect**.
4. Select the branch you want to deploy, then click **Deploy Branch**.
5. The deployment process should happen smoothly if all deployment files are fully functional. Click the button **Open App** at the top of the page to access your App.
6. If the slug size is too large, then add large files not required for the app to the `.slugignore` file.
