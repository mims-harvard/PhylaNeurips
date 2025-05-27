# Tree Reasoning Benchmark

The **Tree Reasoning Benchmark** consists of two tasks across three datasets. It evaluates a model's ability in:

1. **Phylogenetic Tree Reconstruction**  
   - Measured by **normalized Robinson-Foulds distance** (**norm-RF**).

2. **Taxonomic Clustering**  
   - Measured by **cluster completeness** and **Normalized Mutual Information** (**NMI**).

---

## 📦 Download Instructions

To download the benchmark datasets, visit:

👉 [Harvard Dataverse - Tree Reasoning Benchmark (DRAFT)](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi%3A10.7910%2FDVN%2FRKZWLQ&version=DRAFT)

---

## Task 1: Tree Reconstruction

**Benchmarking Approach:**

- Compute the **pairwise distance matrix** from protein embeddings.
- Use the **Neighbor Joining algorithm** to construct a phylogenetic tree.
- Compare against the ground truth using **norm-RF**.

**Datasets Used:**

- `TreeFam`
- `TreeBASE`

### TreeBASE Details

- After downloading and unzipping, you'll find two directories: `sequences/` and `trees/`.
- Filenames are aligned: for example, the tree for `TB2/S137_processed.fa` in `sequences/` is `TB2/S137_processed_tree.nh` in `trees/`.

### TreeFam Details

- After unzipping, you receive a **pickle file**.
- Each key corresponds to a sequence/tree name.
- Each entry contains:
  - `sequences`: the protein sequences
  - `tree_newick`: the Newick-formatted tree

> ⚠️ **Note**: Trees from TreeFam require formatting before use. A formatting script is provided in the evaluation code. If there is enough interest in the benchmark, preprocessed trees can be generated to avoid this step.

---

## Task 2: Taxonomic Clustering

**Benchmarking Approach:**

- Perform **k-means clustering** on protein embeddings.
- Evaluate using:
  - **Cluster Completeness**
  - **Normalized Mutual Information (NMI)**

**Dataset Used:**

- `GTDB` (Genome Taxonomy Database)

### GTDB Details

- After extracting the tar file, you'll find a series of `.tsv` and `.pickle` files with names like:
  - `sampled_bac120_taxonomy_class_0.tsv`
  - `sampled_bac120_taxonomy_class_sequences_0.pickle`

- The structure of these filenames follows the format:
  - `sampled_bac120_taxonomy_[level]_[replicate].tsv`
  - `sampled_bac120_taxonomy_[level]_sequences_[replicate].pickle`

  Where:
  - `[level]` refers to the **taxonomic rank** (e.g., class, order, family).
  - `[replicate]` is a numeric index indicating a random sampling replicate.

- Each `.tsv` file contains:
  - Sequence names
  - Taxonomic labels at the specified level

- The corresponding `.pickle` file contains the actual sequences for those entries.

> Each replicate includes random groupings of 50 distinct labels, with 10 sequences per label. Use the taxonomic column in the `.tsv` and the sequence names to extract the clustering labels.


