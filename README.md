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


### EdNet
Data pre-process for EdNet dataset. we use the 'ednet-kt1' dataset. You can download it [here](https://drive.google.com/file/d/1AmGcOs5U31wIIqvthn9ARqJMrMTFTcaw/view). The question information file is [here](https://drive.google.com/file/d/117aYJAWG3GU48suS66NPaB82HwFj6xWS/view). For more information about [EdNet](https://github.com/riiid/ednet)


### Installation
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/CRO-KT.git
   cd CRO-KT
   python cro_dkt
