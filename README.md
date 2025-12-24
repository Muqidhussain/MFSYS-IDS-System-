# MFSYS Network Traffic Intrusion Detection System (IDS)

## Project Overview

This project presents a **Network Traffic Intrusion Detection System (IDS)** using **machine learning (ML) and deep learning (DL) techniques**.  
The system is designed to detect malicious network activities and classify traffic into two categories:

1. **Normal traffic**  
2. **Attack traffic**  

The main goal is to develop a **highly accurate model** capable of **real-time intrusion detection** on network flows.

---

## Dataset Details

The dataset consists of **134,094 network traffic samples** collected from multiple sources and includes a mix of normal and malicious traffic types.  

### Key Features:

| Feature          | Description                                  |
|-----------------|----------------------------------------------|
| `src_ip`         | Source IP address                            |
| `dst_ip`         | Destination IP address                       |
| `protocol`       | Protocol type (TCP/UDP/etc.)                |
| `packet_length`  | Size of the packet in bytes                  |
| `ttl`            | Time-to-live value of the packet            |
| `src_port`       | Source port number                           |
| `dst_port`       | Destination port number                      |
| `tcp_flags`      | TCP flags (S, A, PA, RA, etc.)              |
| `label`          | Traffic label (normal/attack)               |
| `attack_type`    | Type of attack (nikto, nmap, gobuster, etc.) |
| `source_file`    | Source PCAP file name                        |

### Attack Types Included:

- Nikto  
- Nmap  
- Gobuster  
- SQLmap  
- Dirsearch  
- XSS  

---

## Methodology

The project follows a **stepwise workflow**:

1. **Data Loading & Exploration**  
   - Load CSV dataset and explore samples, columns, and data types.  
   - Check for missing values and identify the label column.

2. **Label Encoding & Feature Cleaning**  
   - Dropped unnecessary columns like `source_file`.  
   - Converted `attack_type` into **binary labels**:
     - `0` → Normal traffic  
     - `1` → Attack traffic  

3. **Categorical Feature Encoding**  
   - Dropped IP address columns (`src_ip`, `dst_ip`).  
   - One-hot encoded `tcp_flags`.

4. **Train/Test Split & Feature Scaling**  
   - Split dataset into **training (80%)** and **testing (20%)** sets.  
   - Applied **StandardScaler** for normalization.

5. **Model Training & Evaluation**  
   - **Random Forest**  
   - **XGBoost**  
   - **MLP (Deep Learning)**  

6. **Flow-Level Feature Engineering**  
   - Aggregate packet-level statistics per flow:
     - Mean, Max, Min, Std of packet_length  
     - Mean, Std of TTL  
     - Source/Destination port counts  
   - One-hot encoding of TCP flags for better model performance.

---

## Model Comparison

| Model         | Accuracy | Weighted F1 | Notes |
|---------------|---------|-------------|-------|
| Random Forest | 88.89%  | 0.84        | Good Attack detection |
| XGBoost       | 88.89%  | 0.90        | Slightly better Normal detection |
| MLP           | 77.78%  | 0.78        | Underperformed due to small dataset |

**Observations:**

- Tree-based models (Random Forest & XGBoost) outperform MLP due to the **small size of flow-level dataset**.  
- XGBoost achieved the **best overall F1-score**, making it suitable for deployment.

---

## Visualizations

- **Bar charts** comparing Accuracy and F1-Weighted scores  
- **Confusion matrices** for all models to evaluate class-wise performance  
- **Combined bar chart** for quick comparison of metrics  

---

## Deployment Potential

The trained **XGBoost model** can be deployed for **real-time network monitoring**:

- Fast inference for live traffic flows  
- High detection rate for attacks  
- Integrable into network IDS systems  

**Future Enhancements:**

- Collect more flows to improve DL models  
- Sequence-based packet features for CNN-LSTM analysis  
- Real-time deployment with continuous learning for evolving threats  

---

## Repository Structure

