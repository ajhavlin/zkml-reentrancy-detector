# Proof of ML Inference for Reentrancy Detection in Solidity Smart Contracts

This repository contains the datasets and notebook for a final-year undergraduate project that integrates machine learning-based vulnerability detection with zero-knowledge proof techniques. The goal is to detect reentrancy vulnerabilities in Solidity smart contracts and produce a verifiable proof of the inference process using EZKL and Halo2 circuits.

## Overview

The project addresses a critical need in smart contract security: providing an efficient and trustless pre-screening for vulnerabilities. Traditional static and symbolic analysis tools (e.g., ESBMC, Slither, Mythril, Oyente) can detect known vulnerability patterns but often lack the ability to produce independently verifiable certificates of their analysis. By combining a convolutional neural network (CNN) with a zero-knowledge proof of inference, our approach ensures that the classification is carried out correctly, without revealing sensitive smart contract code. 

Key components include:
- **Solidity Lexer and Feature Extraction:** A lexer processes Solidity source code to extract relevant tokens and features used as input to the CNN. The implementation draws on methodologies described in Tchang (2020) [1] and Harer et al. (2018) [2].
- **Two-Layer Convolutional Neural Network (CNN):** The model classifies smart contract functions as either vulnerable or safe with respect to reentrancy.
- **Zero-Knowledge Proof of Inference:** Using the EZKL Python tool, the project sets up, proves, and verifies that the ML model’s inference was performed correctly, providing a succinct cryptographic certificate.
- **Datasets:** The project uses a curated dataset of Solidity smart contract functions and corresponding vulnerability labels, compiled from multiple open-source repositories.

## File Structure

- **`Project_Notebook.ipynb`**  
  A comprehensive Jupyter Notebook detailing:
  - The lexer implementation and feature extraction process.
  - Model initialisation, training, evaluation, and the integration of EZKL for generating, proving, and verifying zero-knowledge proofs.
  
- **`reentrancyContracts.py`**  
  Contains the dataset of Solidity smart contract functions.

- **`reentrancyContractLabels.py`**  
  Contains the corresponding labels indicating the presence or absence of reentrancy vulnerabilities in each function.

## Setup and Usage

1. **Clone the Repository:**
```bash
   git clone https://github.com/ajhavlin/zkml-reentrancy-detector.git
   cd zkml-reentrancy-detector
```

2. **Install Dependencies:** Ensure Python 3.8+ is installed, then install the required packages:
```bash
pip install -r requirements.txt
```
Dependencies include libraries such as NumPy, PyTorch (or TensorFlow), and EZKL.

3. **Run the Project Notebook:** Open and run `Project_Notebook.ipynb` to execute the lexer, train and evaluate the CNN model, and perform the ZK proof setup, proof generation, and verification steps.
```bash
jupyter notebook Project_Notebook.ipynb
```

4. **EZKL Integration:** Follow the instructions in the notebook to set up the EZKL environment. This includes:
- Configuring the neural network for ZK proof compatibility.
- Generating a proof of correct inference.
- Verifying the proof to ensure integrity and trustworthiness of the model’s prediction.
Warning: the ZK proof is very computationally intensive and may require running on a dedicated backend such as EZKL’s Lilith API (https://app.ezkl.xyz/). 

## References

1. Tchang, Luke (2020). _Reentrancy Detector for Solidity Smart Contracts. Stanford CS230 Deep Learning Project Report. Available at: [https://cs230.stanford.edu/projects_fall_2020/reports/55027434.pdf](https://cs230.stanford.edu/projects_fall_2020/reports/55027434.pdf) (Accessed: 13/03/2025)._  
    (Referenced for the lexer implementation and dataset preparation.)

2. Harer, Jacob A. et al. (2018). _Automated Software Vulnerability Detection with Machine Learning. ArXiv abs/1803.04497._  
    (Referenced within [1].)

**Dataset References:**

- Final Curated Dataset. Retrieved from: [https://github.com/luketchang/Solidity-Reentrancy-Detector](https://github.com/luketchang/Solidity-Reentrancy-Detector). _(Accessed: 13/03/2025)_.
- SB Curated Data Repository. Retrieved from: [https://github.com/smartbugs/smartbugs-curated/tree/main/dataset](https://github.com/smartbugs/smartbugs-curated/tree/main/dataset). _(Accessed: 13/03/2025)_.
- GNNSCVulDetector Data Repository. Retrieved from: [https://github.com/vntchain/GNNSCVulDetector](https://github.com/vntchain/GNNSCVulDetector). _(Accessed: 13/03/2025)_.
- SolidiFI Benchmark Data Repository. Retrieved from: [https://github.com/smartbugs/SolidiFI-benchmark](https://github.com/smartbugs/SolidiFI-benchmark). _(Accessed: 13/03/2025)_.

## License

This project is licensed under the MIT License. See the LICENSE file for details.