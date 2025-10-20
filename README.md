Email:xlxiang@ustc.edu.cn

# CRO-KT: Cognitive Representation Optimization for Knowledge Tracing

The CRO-KT model designs a coordination and collaboration optimization module, establishes bipartite graph relationship embedding, forms optimal cross-knowledge solution combinations, and fully leverages the advantages of graphs.


## Overview
The model achieves the refinement of cognitive representations through "dual-module optimization + bipartite graph embedding fusion", with its core structure consisting of three parts:

 #### 1) Coordination Module
Based on a dynamic programming algorithm, it targets questions "within the same knowledge point and with significant difficulty differences (|difficulty difference| ≥ α, α ≈ 0.8)". By minimizing the cost function , it adjusts the answer states to address the incoherence issues such as "incorrect answers to easy questions but correct answers to difficult ones" or "correct answers to easy questions but incorrect answers to difficult ones". This ensures that the representations align with students' cognitive patterns (i.e., answering a more difficult question correctly better reflects mastery of easier questions).

 #### 2) Collaboration Module
Based on a co-optimization algorithm, it focuses on questions "within the same knowledge point and with similar difficulty (|difficulty difference| ≤ β, β ≈ 0.05)". It calculates the discriminant coefficient γ (integrating the collaboration strength λ_ij and propagation strength ω_ij between sub-goals) to iteratively optimize answer states. This resolves the problem of insufficient synergy in answer results and makes the representations of questions with similar difficulty more consistent.

 #### 3) Bipartite Graph Relational Embedding Fusion
It constructs a "question-skill" bipartite graph and learns the relational embeddings between questions and skills through cross-entropy loss. These embeddings are then weighted and fused with the optimized cognitive representations, which enhances the cognitive expression across knowledge points and compensates for the limitations of single-record representations.
  


## Environment Setup

### Prerequisites
- Python 3.7+ (tested with Python 3.7)
- Required libraries (see `requirements.txt`)


## Dataset Description

### 1. ASSIST09
- **Full Name**: Assistment 2009-2010 Skill Builder Data  
- **Domain**: K-12 mathematics education (student-problem interaction data)  
- **Content**: Includes student response records (correctness, response time), problem-skill associations, etc.  
- **Download Links**:  
  - Raw dataset: [ASSIST09 Download](https://drive.google.com/file/d/1NNXHFRxcArrU0ZJSb9BIL56vmUt5FhlE/view)  
  - Official documentation: [ASSIST09 Docs](https://sites.google.com/site/assistmentsdata/home/assistment-2009-2010-data/skill-builder-data-2009-2010)  
- **Preprocessing**:  
  - Script: `data_assist09.py`  
  - Key steps: Filter empty skills, scaffolding problems, and users with few interactions; generate intermediate files such as problem-skill mappings and user interaction sequences.  


### 2. ASSIST12
- **Full Name**: Assistment 2012-2013 Data  
- **Domain**: K-12 mathematics education (extended version of ASSIST09)  
- **Features**: Larger dataset size; combined skills are separated by `$$$` (format difference from ASSIST09).  
- **Download Links**:  
  - Raw dataset: [ASSIST12 Download](https://drive.google.com/file/d/1uY8qG1gkxO73hXw8cBkg5L9hC94HhTgX/view)  
  - Official documentation: [ASSIST12 Docs](https://sites.google.com/site/assistmentsdata/home/assistment-2012-2013-data)  
- **Preprocessing**:  
  - Reference script: `data_assist09.py` (need to adjust the separator to `$$$`)  
  - Key steps: Same as ASSIST09; adapt parsing logic for combined skills to generate intermediate files in consistent formats (e.g., `pro_skill_sparse.npz`, `data.txt`).  


### 3. EdNet
- **Full Name**: EdNet: A Large-Scale Hierarchical Educational Dataset  
- **Domain**: Online education platform interaction data (covers multiple subjects)  
- **Subset**: Uses the `ednet-kt1` subset (dedicated to knowledge tracing tasks).  
- **Download Links**:  
  - Dataset: [ednet-kt1 Download](https://drive.google.com/file/d/1AmGcOs5U31wIIqvthn9ARqJMrMTFTcaw/view)  
  - Question info file: [Question Metadata Download](https://drive.google.com/file/d/117aYJAWG3GU48suS66NPaB82HwFj6xWS/view)  
  - Official repository: [EdNet GitHub](https://github.com/riiid/ednet)  
- **Preprocessing**:  
  - Script: `ednet/data.py`  
  - Key steps: Extract problem-skill mappings and user interaction sequences; calculate problem difficulty features (e.g., average response time, correctness rate).  


### Installation
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/CRO-KT.git
   cd CRO-KT
   python cro_dkt
