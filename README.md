# Goodbooks推荐系统

基于Goodbooks-10k数据集的智能图书推荐系统，实现了多种推荐算法并提供性能评估和对比功能。

## 🚀 功能特性

### 推荐算法
- **协同过滤算法**
  - 基于用户的协同过滤
  - 基于物品的协同过滤
  - 矩阵分解（SVD）
- **基于内容的推荐**
  - 内容相似度推荐
  - 用户画像推荐
  - 混合推荐

### 系统功能
- 📊 **数据统计展示** - 用户数、图书数、交互数、数据稀疏度
- 🎯 **个性化推荐** - 为指定用户生成推荐列表
- ⚖️ **算法对比** - 同时展示多种算法的推荐结果
- 📈 **性能评估** - 使用多种指标评估算法性能
- 💻 **现代化界面** - 响应式设计，优雅的用户体验

### 评估指标
- Precision@K - 精确率
- Recall@K - 召回率
- NDCG@K - 归一化折损累积增益
- Hit Rate@K - 命中率
- MRR - 平均倒数排名

## 📦 环境要求

- Python 3.8+
- 现代浏览器（Chrome, Firefox, Safari, Edge）

## 🛠️ 安装步骤

1. **克隆项目**
   ```bash
   git clone <repository-url>
   cd htt2
   ```

2. **安装依赖**
   ```bash
   pip install -r requirements.txt
   ```

3. **准备数据**
   确保以下数据文件在项目根目录：
   - `train_dataset.csv` - 训练数据（用户-物品交互）
   - `test_dataset.csv` - 测试用户列表

4. **启动系统**
   ```bash
   python app.py
   ```

5. **访问界面**
   打开浏览器访问：http://localhost:5000

## 📊 数据格式

### 训练数据 (train_dataset.csv)
```csv
user_id,item_id
0,257
0,267
...
```

### 测试数据 (test_dataset.csv)
```csv
user_id
0
1
...
```

## 🎮 使用指南

### 1. 首页 - 系统概览
- 查看数据集统计信息
- 了解支持的推荐算法

### 2. 推荐页面
- 输入用户ID或随机选择用户
- 选择推荐算法
- 设置推荐数量
- 查看用户历史和推荐结果

### 3. 算法对比
- 输入用户ID
- 同时查看多种算法的推荐结果
- 对比不同算法的推荐差异

### 4. 性能评估
- 设置评估参数（K值、样本大小）
- 运行算法性能评估
- 查看详细的性能指标表格和可视化图表

## 🔧 API 文档

### 数据统计
```
GET /api/stats
返回：数据集统计信息
```

### 用户信息
```
GET /api/user/<user_id>/items
返回：用户交互的物品列表
```

### 获取推荐
```
GET /api/recommend/<user_id>?algorithm=<algo>&k=<num>
参数：
- algorithm: user_cf, item_cf, matrix_factorization, content_based, profile_based, hybrid
- k: 推荐数量
返回：推荐物品列表
```

### 算法对比
```
GET /api/compare/<user_id>?k=<num>
返回：多种算法的推荐结果
```

### 性能评估
```
GET /api/evaluate?k_values=<values>&sample_size=<size>
参数：
- k_values: 逗号分隔的K值列表，如 "5,10,20"
- sample_size: 评估样本大小
返回：评估结果
```

## 📈 技术架构

### 后端
- **Flask** - Web框架
- **pandas** - 数据处理
- **numpy** - 数值计算
- **scikit-learn** - 机器学习算法
- **scipy** - 科学计算

### 前端
- **HTML5/CSS3** - 界面结构和样式
- **JavaScript** - 交互逻辑
- **Plotly.js** - 数据可视化
- **Font Awesome** - 图标库

### 算法实现
- **协同过滤** - 余弦相似度、矩阵分解
- **基于内容** - TF-IDF权重、用户画像
- **评估指标** - 留一法验证、多种评估指标

## 📁 项目结构

```
htt2/
├── app.py                    # Flask应用主文件
├── requirements.txt          # Python依赖
├── README.md                # 项目说明
├── data/                    # 数据处理模块
│   ├── __init__.py
│   └── data_processor.py
├── models/                  # 推荐算法模块
│   ├── __init__.py
│   ├── collaborative_filtering.py
│   ├── content_based.py
│   └── evaluation.py
├── static/                  # 静态资源
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── main.js
├── templates/               # HTML模板
│   └── index.html
├── train_dataset.csv        # 训练数据
└── test_dataset.csv         # 测试数据
```

## 🎯 算法说明

### 协同过滤
1. **基于用户的协同过滤**：找到与目标用户相似的用户，推荐他们喜欢的物品
2. **基于物品的协同过滤**：基于用户历史交互物品，推荐相似的物品
3. **矩阵分解（SVD）**：通过降维技术学习用户和物品的潜在特征

### 基于内容
1. **内容相似度**：基于物品特征计算相似度
2. **用户画像**：构建用户偏好画像，匹配相似物品
3. **混合推荐**：结合多种方法的优势

## 📊 性能评估

系统使用留一法验证和多种评估指标：

- **Precision@K**：推荐列表中相关物品的比例
- **Recall@K**：用户相关物品中被推荐的比例
- **NDCG@K**：考虑排序质量的评估指标
- **Hit Rate@K**：推荐列表是否包含相关物品
- **MRR**：第一个相关物品的平均倒数排名

## 🤝 贡献指南

1. Fork 项目
2. 创建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📄 许可证

本项目基于Goodbooks-10k公开数据集开发，仅用于学习和研究目的。

## 🔍 常见问题

### Q: 系统启动缓慢？
A: 首次启动时系统需要加载数据和计算相似度矩阵，请耐心等待。后续启动会使用缓存数据。

### Q: 推荐结果为空？
A: 请确保输入的用户ID在训练数据中存在，或尝试使用"随机选择"功能。

### Q: 性能评估时间长？
A: 可以减少样本大小或K值来加快评估速度。

### Q: 如何添加新的推荐算法？
A: 在 `models/` 目录下创建新的算法模块，并在 `app.py` 中添加相应的API端点。

## 📞 支持

如有问题或建议，请通过以下方式联系：
- 提交 Issue
- 发送邮件
- 创建 Pull Request

---

�� 感谢使用Goodbooks推荐系统！ 