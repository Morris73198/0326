# Pseudo code 對應到 mountain car IRL 的地方

1. expert data 輸入以及獲取：
   
pseudocode 第1行 >>> 對應到 train.py 中的
![architecture](Picture1.png)

2. 初始化 policy：
   
pseudocode 第2行 >>> 對應到 train.py 中的
![architecture](Picture2.png)

3. 初始化 IRL 模型（參數）：
   
pseudocode 第3行 >>> 對應到 train.py 中的
![architecture](Picture3.png)

4. 收集環境互動（Collect episode）、更新策略 (Update policy) 、估計獎勵 (Estimate rewards):
   
pseudocode 第10-14行迴圈 >>> 對應到 train.py 中的
![architecture](Picture4.png)

5. 估計獎勵 (Estimate rewards) 、並更新獎勵函數 (Update reward function):
   
pseudocode 第16-17行 >>> 對應到 train.py 中的:
![architecture](Picture5.png)



## 下一步 製作 Expert Data

neuralcomapping 儲存配置

![architecture](Picture6.png)


預計會將 sensor_pose, origin_pose, obstacle, frontier, explored, explorable,  ??reward 放入 expert data 中。

## Data Structure 構想

如果要以 mountaincar 為基礎去修改成 unknown environment exploration 的話, 我們的 policy 架構就必須改為 Q Table。Q-Table是個狀態(state)-動作(action)的互動表。

我們的狀態(state)有 sensor_pose, origin_pose, obstacle, frontier, explored, explorable 以及 reward。

因此我們需要 allocate {num_robot * 3 + num_robot * 3 + map_size * map_size + map_size * map_size + map_size * map_size + map_size * map_size + num_robot} 的大小給 state。

而我們的 action 是要從 forntier 中選取一個點作為下一步的目標點, 因此我們需要 allocate {map_size * map_size} 的大小給 action。

如果以 neuralcomapping 為例, 我們至少必須 allocate {map_size ^ 4 (480 ^ 4)} 的大小給 QTable。
