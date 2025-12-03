# Website Fingerprinting on Anonymous Network

## Introduction

Website Fingerprinting is an attack technique that identifies which websites a user visits by analyzing the size, order, direction, and time patterns of encrypted traffic.

Tor provides anonymity by placing three relays (Guard, Middle, Exit) between the user and the site. However, if an attacker observes the encrypted traffic between the user and the first proxy (Entry Guard), they can infer the visited site through unique traffic patterns left by site-specific content (images, scripts, ads, etc.).

The goal of this project is to create a classifier that learns these patterns using machine learning to classify visited sites, aiming to explore both the Closed-world scenario (assuming only known sites) and the realistic Open-world scenario (including unknown sites).

## Repository Structure

```markdown
.
├── README.md
├── feature_extraction.ipynb
├── closed
│   ├── K-NN.ipynb
│   ├── LR.ipynb
│   ├── LightGBM.ipynb
│   ├── RF.ipynb
│   ├── SVM.ipynb
│   └── XGBoost.ipynb
├── open
│   ├── binary
│   │   ├── K-NN.ipynb
│   │   ├── LR.ipynb
│   │   ├── LightGBM.ipynb
│   │   ├── RF.ipynb
│   │   ├── SVM.ipynb
│   │   └── XGBoost.ipynb
│   └── multi
│       ├── K-NN.ipynb
│       ├── LR.ipynb
│       ├── LightGBM.ipynb
│       ├── RF.ipynb
│       ├── SVM.ipynb
│       └── XGBoost.ipynb
└── extra
```

## Datasets

- mon_standard.pkl: Data from monitored websites.
    - Class count: 95
    - Instance count: 19,000 (95 websites, each with 10 subpages which are non-index pages, observed 20 times each)
- unmon_standard10.pkl: Data from unmonitored websites.
    - Instance count: 10,000
- unmon_standard10_3000.pkl: Data from the unmonitored website, with the number of data samples reduced by 3,000.
    - Instance count: 3,000

## How to Run

### Feature extraction

1. Download datasets: mon_standard.pkl, unmon_standard10.pkl, unmon_standard10_3000.pkl
    Link: https://drive.google.com/drive/folders/13sDplxKUNmntbYr6WhpqQARiBvH41Oum
2. Upload mon_standard.pkl, unmon_standard10.pkl to content folder in Google Colab.
    If you encounter a RAM error due to the data size when using the unmon_standard10.pkl file, please use the unmon_standard10_3000.pkl file instead.
    And then, modify the path of file: /content/unmon_standard10_3000.pkl
3. Download and run feature_extraction.ipynb.
4. Check mon_features.pkl and unmon_features.pkl are created, then download them.

### Closed-world

1. Download code files in closed folder.
2. Upload mon_features.pkl to content folder in Google Colab.
3. Run code files.

### Open-world: Binary classification

1. Download code files in open/binary folder.
2. Upload mon_features.pkl, unmon_features.pkl to content folder in Google Colab.
3. Run code files.

### Open-world: Multi classification

1. Download code files in open/multi folder.
2. Upload mon_features.pkl, unmon_features.pkl to content folder in Google Colab.
3. Run code files.

---

# Extra credit

## Introduction

Extra Credit is designed to test the robustness of WF attacks against active defense mechanisms. Traffic Splitting defenses, including Burst Window Randomization (BWR) attempts to break the unique temporal and volume patterns of a website by fragmenting the traffic across multiple Tor circuits and injecting random delays (BWR), significantly reducing the effectiveness of conventional WF models. Therefore, the traffic patterns applied with this defenses are different from the existing patterns, the existing machine learning models and features show low performance.

The goal of extra credit is evaluating and improving the accuracy of our classification models when the traffic is protected by traffic splitting defenses, including BWR.

## Repository Structure

```markdown
.
└── extra
    ├── data_processing.ipynb
    ├── feature_extraction.ipynb
    ├── closed
    │   ├── K-NN.ipynb
    │   ├── RF.ipynb
    │   └── XGBoost.ipynb
    └── open
        ├── binary
        │   ├── K-NN.ipynb
        │   ├── RF.ipynb
        │   └── XGBoost.ipynb
        └── multi
            ├── K-NN.ipynb
            ├── RF.ipynb
            └── XGBoost.ipynb
```

## Datasets

The BigEnough dataset, which was processd with TrafficSliver BWR and split into five cell files.

- mon.zip: Compressed data from monitored websites.
    - Instance count: 19,000
- unmon.zip: Compressed data from unmonitored websites.
    - Instance count: 19,000

## How to Run

### Data processing

1. Download datasets:
    Link: https://drive.google.com/drive/folders/1SePvqnlridCldmjXbr_TSGigohGT8TXV
2. Upload mon.zip, unmon.zip to content folder in Google Colab.
3. Download data_processing.ipynb in extra folder.
4. Run data_processing.ipynb.
5. Check processed_mon_data.pkl and processed_unmon_data.pkl are created, then download them.

### Feature extraction

1. Download feature_extraction.ipynb in extra folder.
2. Upload processed_mon_data.pkl, processed_unmon_data.pkl to content folder in Google Colab.
3. Run feature_extraction.ipynb.
4. Check extra_mon_features.pkl and extra_features.pkl are created, then download them.

### Closed-world

1. Download code files in extra/closed folder.
2. Upload extra_mon_features.pkl to content folder in Google Colab.
3. Run code files.

### Open-world: Binary classification

1. Download code files in extra/open/binary folder.
2. Upload extra_features.pkl to content folder in Google Colab.
3. Run code files.

### Open-world: Multi classification

1. Download code files in extra/open/multi folder.
2. Upload extra_features.pkl to content folder in Google Colab.
3. Run code files.

---

## Members & Roles

|Kim Min|Park Jieun|Baek Soyoung|Song Youngchae|Cho Hyerim|
|---|---|---|---|---|
|Leader, GiuHub management, SVM model training, extra credit feature extraction|minutes of meeting management, Random Forest model training, extra credit model training|meeting schedule and project requirement compliance management, K-NN model training, extra credit result analysis|code organization and management, XGBoost & LightGBM model training, extra credit data processing|document management, K-NN & Logistic Regression model training|
