**Deep Learning Tips and Tricks translation**

<br>

**1. Deep Learning Tips and Tricks cheatsheet**

&#10230;
深度學習秘訣和技巧參考手冊
<br>


**2. CS 230 - Deep Learning**

&#10230;
CS 230 - 深度學習
<br>


**3. Tips and tricks**

&#10230;
秘訣和技巧
<br>


**4. [Data processing, Data augmentation, Batch normalization]**

&#10230;
[資料處理, 資料擴增, 批次正規化]
<br>


**5. [Training a neural network, Epoch, Mini-batch, Cross-entropy loss, Backpropagation, Gradient descent, Updating weights, Gradient checking]**

&#10230;
[訓練一個神經網路, 週期 (epoch), 小批次 (mini-batch), 交叉熵損失, 反向傳播演算法, 梯度下降法, 更新權重, 梯度檢查]
<br>


**6. [Parameter tuning, Xavier initialization, Transfer learning, Learning rate, Adaptive learning rates]**

&#10230;
[調整參數, Xavier 初始化, 遷移學習, 學習率, 自適應學習率]
<br>


**7. [Regularization, Dropout, Weight regularization, Early stopping]**

&#10230;
[正規化, Dropout, 權重正規化, Early stopping]
<br>


**8. [Good practices, Overfitting small batch, Gradient checking]**

&#10230;
[良好的實踐, 在小批量的資料上過擬合, 確認梯度]
<br>


**9. View PDF version on GitHub**

&#10230;
在 Github 上檢視 PDF 版本
<br>


**10. Data processing**

&#10230;
資料處理
<br>


**11. Data augmentation ― Deep learning models usually need a lot of data to be properly trained. It is often useful to get more data from the existing ones using data augmentation techniques. The main ones are summed up in the table below. More precisely, given the following input image, here are the techniques that we can apply:**

&#10230;
資料擴增 - 深度學習模型通常需要大量的資料進行訓練。將既有的訓練資料透過資料擴增技術來取得更多的資料通常很有用。下表中總結了主要的技術，更精確的說，給定一張原始圖片，我們可以應用的技術如下：
<br>


**12. [Original, Flip, Rotation, Random crop]**

&#10230;
[原始圖片, 翻轉, 旋轉, 隨機裁切]
<br>


**13. [Image without any modification, Flipped with respect to an axis for which the meaning of the image is preserved, Rotation with a slight angle, Simulates incorrect horizon calibration, Random focus on one part of the image, Several random crops can be done in a row]**

&#10230;
[沒有進行任何修改的原始圖片, 僅對於軸進行翻轉，保留圖片原始資訊, 僅行些微的角度旋轉, 模擬不正確的水平校正, 隨機關注圖片的某個部份, 可以對某行連續進行隨機裁切]
<br>


**14. [Color shift, Noise addition, Information loss, Contrast change]**

&#10230;
[色彩偏移, 加入雜訊, 丟失資訊, 改變對比]
<br>


**15. [Nuances of RGB is slightly changed, Captures noise that can occur with light exposure, Addition of noise, More tolerance to quality variation of inputs, Parts of image ignored, Mimics potential loss of parts of image, Luminosity changes, Controls difference in exposition due to time of day]**

&#10230;
[RGB 色彩的些微改變, 捕捉曝光時可能的雜訊, 加入雜訊, 對於輸入圖片有更高的容忍度, 忽略局部的圖片, 模仿圖片部分的資訊丟失, 改變亮度, 控制在一天中不同時間造成的曝光差異]
<br>


**16. Remark: data is usually augmented on the fly during training.**

&#10230;
注意：資料通常是在模型訓練階段即時進行
<br>


**17. Batch normalization ― It is a step of hyperparameter γ,β that normalizes the batch {xi}. By noting μB,σ2B the mean and variance of that we want to correct to the batch, it is done as follows:**

&#10230;
批次正規化 - 它是一個藉由 γ,β 兩個超參數來正規化每個批次 {xi} 的過程。每一次正規化的過程，我們使用 μB,σ2B 分別代表平均數和變異數。請參考以下公式：
<br>


**18. It is usually done after a fully connected/convolutional layer and before a non-linearity layer and aims at allowing higher learning rates and reducing the strong dependence on initialization.**

&#10230;
批次正規化的動作通常在全連接層/卷積層之後、在非線性層之前進行。目的在於接納更高的學習速率，並且減少該批次學習初期對取樣資料特徵的依賴性。
<br>


**19. Training a neural network**

&#10230;
訓練一個神經網路
<br>


**20. Definitions**

&#10230;
定義
<br>


**21. Epoch ― In the context of training a model, epoch is a term used to refer to one iteration where the model sees the whole training set to update its weights.**

&#10230;
(週期) Epoch - 在訓練模型時，當模型看過整個訓練資料集一次，並且更新對應的模型權重稱之為一個週期 (epoch)
<br>

**22. Mini-batch gradient descent ― During the training phase, updating weights is usually not based on the whole training set at once due to computation complexities or one data point due to noise issues. Instead, the update step is done on mini-batches, where the number of data points in a batch is a hyperparameter that we can tune.**

&#10230;
小批次 (mini-batch) 梯度下降 - 在訓練階段，通常不會使用整個訓練資料集來更新權重，因為需要耗費太多計算資源，也不會使用單一資料點，因為單一資料有可能會有雜訊。我們會使用一個小批次的資料來更新權重，而要選取多少資料當成一個小批次，則是可以透過超參數來進行調整。
<br>


**23. Loss function ― In order to quantify how a given model performs, the loss function L is usually used to evaluate to what extent the actual outputs y are correctly predicted by the model outputs z.**

&#10230;
損失函數 - 為了量化模型的表現，損失函數 L 通常用來計算預測值 z 和實際值 y 之間的差距量
<br>


**24. Cross-entropy loss ― In the context of binary classification in neural networks, the cross-entropy loss L(z,y) is commonly used and is defined as follows:**

&#10230;
交叉熵損失函數 - 在二元分類的情境中，交叉熵損失函數 L(z,y) 經常被使用，定義如下：
<br>


**25. Finding optimal weights**

&#10230;
尋找最佳權重
<br>


**26. Backpropagation ― Backpropagation is a method to update the weights in the neural network by taking into account the actual output and the desired output. The derivative with respect to each weight w is computed using the chain rule.**

&#10230;
反向傳播演算法 - 反向傳播演算法是一種在神經網路中用來更新權重的方法，更新的基準是根據神經網路的實際輸出值和期望輸出值之間的關係。權重的導數是根據連鎖律 (chain rule) 來計算。
<br>


**27. Using this method, each weight is updated with the rule:**

&#10230;
透過這種方法，每一個權重更新的方式如下：
<br>


**28. Updating weights ― In a neural network, weights are updated as follows:**

&#10230;
更新權重 - 在神經網路中，權重更新的步驟如下：
<br>


**29. [Step 1: Take a batch of training data and perform forward propagation to compute the loss, Step 2: Backpropagate the loss to get the gradient of the loss with respect to each weight, Step 3: Use the gradients to update the weights of the network.]**

&#10230;
[步驟一：取出一個批次 (batch) 的資料，執行前向傳播演算法 (forward propagation) 來得到對應的損失值。步驟二：將損失值透過反向傳播演算法來得到梯度。步驟三：使用梯度來更新網路的權重]
<br>


**30. [Forward propagation, Backpropagation, Weights update]**

&#10230;
[前向傳播演算法, 反向傳播演算法, 權重更新]
<br>


**31. Parameter tuning**

&#10230;
調整參數
<br>


**32. Weights initialization**

&#10230;
初始化參數
<br>


**33. Xavier initialization ― Instead of initializing the weights in a purely random manner, Xavier initialization enables to have initial weights that take into account characteristics that are unique to the architecture.**

&#10230;
Xavier 初始化 - Xavier 初始化可以考慮網路架構獨特的特性，而不是純粹以隨機的方式來進行權重的初始化。
<br>


**34. Transfer learning ― Training a deep learning model requires a lot of data and more importantly a lot of time. It is often useful to take advantage of pre-trained weights on huge datasets that took days/weeks to train, and leverage it towards our use case. Depending on how much data we have at hand, here are the different ways to leverage this:**

&#10230;
遷移學習 - 訓練一個神經網路模型需要大量的資料和時間。在大多的情況下，如果可以在需要訓練數天/週的龐大資料集上使用預訓練好的參數，並將其運用在我們自身的案例上時，是很有用的。根據我們手上有多少資料，有以下幾種方法：
<br>


**35. [Training size, Illustration, Explanation]**

&#10230;
[訓練資料大小, 圖示, 解釋]
<br>


**36. [Small, Medium, Large]**

&#10230;
[小, 中, 大]
<br>


**37. [Freezes all layers, trains weights on softmax, Freezes most layers, trains weights on last layers and softmax, Trains weights on layers and softmax by initializing weights on pre-trained ones]**

&#10230;
[凍結所有層, 透過 softmax 來訓練權重, 凍結大多層, 透過最後一層和 softmax 來訓練權重, 透過所有的層和 softmax，在預先訓練好的權重上進行訓練]
<br>


**38. Optimizing convergence**

&#10230;
最佳化收斂
<br>


**39. Learning rate ― The learning rate, often noted α or sometimes η, indicates at which pace the weights get updated. It can be fixed or adaptively changed. The current most popular method is called Adam, which is a method that adapts the learning rate.**

&#10230;
學習速率 - 學習速率通常用 α 或 η 來表示，目的是用來控制權重更新的速度。學習速度可以是一個固定值，或是隨著訓練的過程改變。現在最熱門的最佳化方法叫作 Adam，是一種隨著訓練過程改變學習速率的最佳化方法。
<br>


**40. Adaptive learning rates ― Letting the learning rate vary when training a model can reduce the training time and improve the numerical optimal solution. While Adam optimizer is the most commonly used technique, others can also be useful. They are summed up in the table below:**

&#10230;
動態調整學習速率 - 訓練模型時，讓學習速率進行變化可以減少訓練時間，同時改善數值最佳解。儘管 Adam 是最常使用的優化器，但其他的方法也可能有用。這些方法匯總如下：
<br>


**41. [Method, Explanation, Update of w, Update of b]**

&#10230;
[方法, 解釋, 更新 w, 更新 b]
<br>


**42. [Momentum, Dampens oscillations, Improvement to SGD, 2 parameters to tune]**

&#10230;
[動量, 阻尼振盪, SGD 的改善, 有兩個參數要調整]
<br>


**43. [RMSprop, Root Mean Square propagation, Speeds up learning algorithm by controlling oscillations]**

&#10230;
[RMSprop, 均方根傳播, 透過控制震盪來加快學習演算法]
<br>


**44. [Adam, Adaptive Moment estimation, Most popular method, 4 parameters to tune]**

&#10230;
[Adam, 自適應估計, 最熱門的方法, 有四個參數要調整]
<br>


**45. Remark: other methods include Adadelta, Adagrad and SGD.**

&#10230;
注意：其他的方法還有 Adadelta、Adagrad 和 SGD。
<br>


**46. Regularization**

&#10230;

<br>


**47. Dropout ― Dropout is a technique used in neural networks to prevent overfitting the training data by dropping out neurons with probability p>0. It forces the model to avoid relying too much on particular sets of features.**

&#10230;

<br>


**48. Remark: most deep learning frameworks parametrize dropout through the 'keep' parameter 1−p.**

&#10230;

<br>


**49. Weight regularization ― In order to make sure that the weights are not too large and that the model is not overfitting the training set, regularization techniques are usually performed on the model weights. The main ones are summed up in the table below:**

&#10230;

<br>


**50. [LASSO, Ridge, Elastic Net]**

&#10230;

<br>

**50 bis. Shrinks coefficients to 0, Good for variable selection, Makes coefficients smaller, Tradeoff between variable selection and small coefficients]**

&#10230;

<br>

**51. Early stopping ― This regularization technique stops the training process as soon as the validation loss reaches a plateau or starts to increase.**

&#10230;

<br>


**52. [Error, Validation, Training, early stopping, Epochs]**

&#10230;

<br>


**53. Good practices**

&#10230;

<br>


**54. Overfitting small batch ― When debugging a model, it is often useful to make quick tests to see if there is any major issue with the architecture of the model itself. In particular, in order to make sure that the model can be properly trained, a mini-batch is passed inside the network to see if it can overfit on it. If it cannot, it means that the model is either too complex or not complex enough to even overfit on a small batch, let alone a normal-sized training set.**

&#10230;

<br>


**55. Gradient checking ― Gradient checking is a method used during the implementation of the backward pass of a neural network. It compares the value of the analytical gradient to the numerical gradient at given points and plays the role of a sanity-check for correctness.**

&#10230;

<br>


**56. [Type, Numerical gradient, Analytical gradient]**

&#10230;

<br>


**57. [Formula, Comments]**

&#10230;

<br>


**58. [Expensive; loss has to be computed two times per dimension, Used to verify correctness of analytical implementation, Trade-off in choosing h not too small (numerical instability) nor too large (poor gradient approximation)]**

&#10230;

<br>


**59. ['Exact' result, Direct computation, Used in the final implementation]**

&#10230;

<br>


**60. The Deep Learning cheatsheets are now available in [target language].

&#10230;


**61. Original authors**

&#10230;

<br>

**62.Translated by X, Y and Z**

&#10230;

<br>

**63.Reviewed by X, Y and Z**

&#10230;

<br>

**64.View PDF version on GitHub**

&#10230;

<br>

**65.By X and Y**

&#10230;

<br>
