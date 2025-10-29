# SC4000-Project
# SC4000/CZ4041/CE4041 - MCTS Strength Prediction Project

这个仓库是我们团队的项目代码库。

## 快速开始

- 系统要求：Python 3.11（建议）或兼容版本
- 推荐使用虚拟环境隔离依赖

1) 克隆并进入项目目录
```bash
git clone <你的仓库地址>
cd SC4000-Project
```

2) 创建并激活虚拟环境
```bash
python3 -m venv .venv && source .venv/bin/activate
```

3) 安装依赖
```bash
pip install -r mcts_strength_prediction/requirements.txt
```

4) 启动 Jupyter（如需运行 Notebook）
```bash
python -m jupyter notebook
```

可选：将当前虚拟环境注册为 Jupyter 内核，方便在 Notebook 中选择
```bash
python -m ipykernel install --user --name sc4000-venv --display-name ".venv"
```

---


## 依赖与环境

以下依赖已在 `mcts_strength_prediction/requirements.txt` 中列出：

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- lightgbm
- xgboost（LightGBM 在 macOS 下异常时的替代）
- jupyter
- ipykernel

安装依赖：
```bash
pip install -r mcts_strength_prediction/requirements.txt
```

macOS 下使用 LightGBM 需要安装 OpenMP：
```bash
brew install libomp
```

如遇 LightGBM 动态库加载错误（`libomp.dylib` not found），先安装 `libomp`，再重装 LightGBM：
```bash
pip uninstall -y lightgbm && pip install lightgbm
```

---

## 📊 数据集说明与获取 (Dataset)

我们项目使用的数据分为两部分：原始数据和经过增强处理后的数据。

**1. 原始数据 (Raw Data)**

*   请从Kaggle竞赛官网下载原始数据文件 (`train.csv`, `test.csv`等)。
*   在项目根目录下创建一个名为 `data/` 的文件夹。
*   将下载的所有原始 `.csv` 文件放入 `data/` 文件夹中。

**2. 增强后的训练数据集 (Augmented Training Data) - 【重要！】**

我们的模型训练**必须**基于经过EDA处理和数据增强后的数据集 `train_augmented.csv`。

你有两种方式获取这个文件：

*   **方式A: 直接下载 (推荐)**
    *   我们已经将生成好的最终数据集存放在了Google Drive上。
    *   **下载链接**: https://drive.google.com/file/d/1z6e-X0kNd4vCqwfNjg2sG87qet9OK_RW/view?usp=drive_link
    *   下载后，请将其也放入项目根目录下的 `data/` 文件夹中。

*   **方式B: 自行生成 (用于验证或修改)**
    *   如果你想了解数据处理的全过程，或者需要对流程进行修改，可以自行生成。
    *   运行位于 `notebooks/` 文件夹下的 `01_EDA_and_Data_Augmentation.ipynb`。
    *   **注意**: 运行前请确保原始数据已按要求放在 `data/` 文件夹内。脚本的最终输出就是 `train_augmented.csv`。

## 📁 项目结构

-   `data/`: (本地文件夹，被.gitignore忽略) 用于存放所有数据文件。
-   `notebooks/`: 存放我们的探索性分析和数据处理的Jupyter Notebooks。
-   `src/`: 存放可复用的Python脚本（如特征工程函数、模型训练脚本）。
-   `README.md`: 项目说明文档。

## 👨‍💻 团队成员工作流程

*   **特征工程师**:
    1.  从方式A下载 `train_augmented.csv`。
    2.  在 `notebooks/` 中创建你自己的实验Notebook，基于 `train_augmented.csv` 开发新的特征。
    3.  将成熟的特征生成函数，沉淀到 `src/feature_engineering.py` 脚本中。

*   **建模工程师**:
    1.  从方式A下载 `train_augmented.csv`。
    2.  在 `src/train.py` 脚本中，加载 `train_augmented.csv`，并调用特征工程脚本，开始你的模型训练和验证工作。