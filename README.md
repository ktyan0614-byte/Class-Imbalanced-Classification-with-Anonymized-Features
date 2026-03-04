# General Binary Classification Model
**國立成功大學 資料科學導論 預測競賽 - 亞軍 (2nd Place / 66 Teams)**

## 🎯 競賽任務與核心挑戰 (Task & Challenges)
本次競賽有別於單一資料集的預測，官方提供了**多個包含大量匿名特徵、且資料分佈各自不同的獨立資料集**。
* **技術挑戰**：參賽者無法依賴特定領域知識 (Domain Knowledge) 進行人工特徵工程。
* **評估規則**：最終排名並非看單一資料集，而是看模型在「所有資料集上預測 AUC 表現的加權平均」。
* **核心目標**：必須建構出一套具有極高**「Generalization」**與**Robustness」**的機器學習 Pipeline ，確保同一套模型架構能在各種未知的測試數據上都保持高水準的預測能力。

## 🏅 競賽成果與核心亮點
* **最終排名**：在全班 66 組參賽隊伍中，脫穎而出榮獲 **第 2 名 (Top 3%)**。
* **評估指標 **：ROC-AUC (Area Under the ROC Curve)。
* **排行榜逆襲與抵禦過擬合 (Leaderboard Shake-up & Overfitting Prevention)**：
  在面對多種未知分佈的資料時，許多隊伍為了迎合公開測試集 (Public Dataset) 而過度調參，發生了嚴重的過擬合。本專案透過嚴謹的交叉驗證 (5-Fold CV) 與模型集成，展現了極強的泛化能力：
  * **Public 前段班的群體過擬合**：在 Public Leaderboard 排名前 9 名的領先群隊伍，面對未知的 Private 測試集時遭遇了嚴重的分數崩跌，**平均 AUC 衰退幅度高達 `0.028`**。
  * **本專案的極致穩定性**：本專案拒絕盲目追高 Public 分數，模型表現極度穩健。在 Private 結算時，**AUC 衰退幅度僅 `0.013` (不到領先群平均的一半)**，憑藉極低的效能損耗率成功逆襲，以 Private AUC `0.8617` 奪得亞軍。這項數據完美驗證了「Robustness」在真實機器學習專案中的決定性價值。
## 🛠️ 核心技術與模型架構 (Tech Stack)
* **演算法**：`XGBoost`, `LightGBM`, `CatBoost`, `RandomForest`
* **模型集成 (Ensemble Learning)**：使用 `Soft Voting Classifier` 融合多個異質性強大的梯度提升樹 (GBDT) 模型，並給予不同權重 (XGBoost : CatBoost : LightGBM=1.5 : 1.5 :1 )。
* **驗證策略**：`5-Fold Stratified K-Fold Cross Validation`，確保在資料不平衡的情況下，訓練集與驗證集的正負樣本比例一致。
* **超參數優化**：利用 `RandomizedSearchCV` 進行自動化調參。

## 📁 資料集與重現聲明 (Dataset Statement)
> **注意：本專案未包含訓練與測試資料集。**

基於學術競賽規範與資料隱私，且競賽官方**未公開測試集的真實標籤 (Ground Truth)**，本 Repository 僅提供資料處理與模型訓練的核心原始碼。

