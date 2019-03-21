# CSFX HW 2

```
Team #15
107062503 許博皓
107062513 鄭家鈞
107062566 黃鈺程
```
## MUNIT

MUNIT 對於 UNIT 做出了改進。UNIT 設計為解決未 1-to-1 的 domain 轉換。而 MUNIT 可以做 1-to-many 的轉換。有別於傳統的 GAN，這兩個方法都不需要準備好 **成對** 的 images，只需各個 domain 的一些圖片，這大大地降低了圖片收集的成本。

### Intuition

在進行圖片轉換時，MUNIT 認為圖片可以由 **Content Code** 與 **Style Code** 表示。其中 Content Code 是 domain-invariant 的，而 Style Code 是 domain-specific 的。如果要將圖片從 Domain A 轉至 Domain B，我們只需結合該圖片的 Content Code 與 Domain B 中隨機一個 Style Code。

難點在於如何將圖拆解得好？如果結合得好？MUNIT 採用了 UNIT 延申自 AutoEncoder 的架構，並根據 Content Code 與 Style Code 的特性不同做出了許多調整。

### Architecture

$X_1, X_2$ 代表不同 Domain，$C$ 是 Content Code Space，$S$ 是 Style Code Space，值得注意的是 Content Code Space 是共同。

**拆解示意圖**：
![](https://i.imgur.com/CQUyWpr.png)

**結合示意圖**：
![](https://i.imgur.com/Ksima2b.png)


### Loss

Loss 由二項組成：
1. `bidirectional reconstruction loss`: 確保 encoder 與 decoder 互為反函數。
2. `adversarial loss`: 確保資料分佈在轉換 domain 時保持一致。

![](https://i.imgur.com/DJcfb5k.png)


完整的 objectives 為：

![](https://i.imgur.com/jV2GFow.png)


### Training

## Introduction

## Results:
跑了10天大約770000個iterations…
![](https://i.imgur.com/X7xFq7x.png)

### Yosemite summer2winter
#### summer -> winter

| Input                                |                                      |                                      |
|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/A1CenWo.jpg) |                                      |                                      |
| Output                               |                                      |                                      |
| ![](https://i.imgur.com/JHuNRkU.jpg) | ![](https://i.imgur.com/ScHZcha.jpg) | ![](https://i.imgur.com/2PdlGEC.jpg) |
| ![](https://i.imgur.com/wcJUeX5.jpg) | ![](https://i.imgur.com/Vnthvt2.jpg) | ![](https://i.imgur.com/qcF8Ji4.jpg) |
| ![](https://i.imgur.com/hwSrU75.jpg) | ![](https://i.imgur.com/EAE8L70.jpg) | ![](https://i.imgur.com/NpCx2Hb.jpg) |

<!-- ![](https://i.imgur.com/A1CenWo.jpg)
![](https://i.imgur.com/JHuNRkU.jpg)
![](https://i.imgur.com/ScHZcha.jpg)
![](https://i.imgur.com/2PdlGEC.jpg)
![](https://i.imgur.com/wcJUeX5.jpg)
![](https://i.imgur.com/Vnthvt2.jpg)
![](https://i.imgur.com/qcF8Ji4.jpg)
![](https://i.imgur.com/hwSrU75.jpg)
![](https://i.imgur.com/EAE8L70.jpg)
![](https://i.imgur.com/NpCx2Hb.jpg) -->

#### winter -> summer
<!-- ![](https://i.imgur.com/FswR3D3.jpg)
![](https://i.imgur.com/o1yW1ww.jpg)
![](https://i.imgur.com/ffTSCeh.jpg)
![](https://i.imgur.com/rWDM9M7.jpg)
![](https://i.imgur.com/OAHOpwq.jpg)
![](https://i.imgur.com/PFjwu41.jpg)
![](https://i.imgur.com/k4TI20a.jpg)
![](https://i.imgur.com/5r87cmj.jpg)
![](https://i.imgur.com/oIGw8TZ.jpg)
![](https://i.imgur.com/ee5pjzP.jpg) -->

| Input                                |                                      |                                      |
|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/FswR3D3.jpg) |                                      |                                      |
| Output                               |                                      |                                      |
| ![](https://i.imgur.com/o1yW1ww.jpg) | ![](https://i.imgur.com/ffTSCeh.jpg) | ![](https://i.imgur.com/rWDM9M7.jpg) |
| ![](https://i.imgur.com/OAHOpwq.jpg) | ![](https://i.imgur.com/PFjwu41.jpg) | ![](https://i.imgur.com/k4TI20a.jpg) |
| ![](https://i.imgur.com/5r87cmj.jpg) | ![](https://i.imgur.com/oIGw8TZ.jpg) | ![](https://i.imgur.com/ee5pjzP.jpg) |

### edges2handbags
#### edge -> handbags
| Input                                |                                      |                                      |
|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/GEP0b4s.jpg) |                                      |                                      |
| Output                               |                                      |                                      |
| ![](https://i.imgur.com/jxKMtBs.jpg) | ![](https://i.imgur.com/7uSHwCK.jpg) | ![](https://i.imgur.com/8cEfh50.jpg) |
| ![](https://i.imgur.com/u2Sq0qw.jpg) | ![](https://i.imgur.com/JN8Mk3Q.jpg) | ![](https://i.imgur.com/u3NRKG3.jpg) |
| ![](https://i.imgur.com/khfBkFd.jpg) | ![](https://i.imgur.com/JQs0tP3.jpg) | ![](https://i.imgur.com/GQpP9Qe.jpg) |

#### handbag -> edges
| Input                                |                                      |                                      |
|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/sAZRQHI.jpg) |                                      |                                      |
| Output                               |                                      |                                      |
| ![](https://i.imgur.com/CX5kmpu.jpg) | ![](https://i.imgur.com/l0xiZUU.jpg) | ![](https://i.imgur.com/724GFnT.jpg) |
| ![](https://i.imgur.com/2gUR4SI.jpg) | ![](https://i.imgur.com/Kjwtbv8.jpg) | ![](https://i.imgur.com/2jsOGKU.jpg) |
| ![](https://i.imgur.com/XKlq97e.jpg) | ![](https://i.imgur.com/HlIi6SW.jpg) | ![](https://i.imgur.com/8Wry0uo.jpg) |
<!-- 
![](https://i.imgur.com/sAZRQHI.jpg)![](https://i.imgur.com/CX5kmpu.jpg)
![](https://i.imgur.com/l0xiZUU.jpg)![](https://i.imgur.com/724GFnT.jpg)
![](https://i.imgur.com/2gUR4SI.jpg)![](https://i.imgur.com/Kjwtbv8.jpg)
![](https://i.imgur.com/2jsOGKU.jpg)![](https://i.imgur.com/XKlq97e.jpg)
![](https://i.imgur.com/HlIi6SW.jpg)![](https://i.imgur.com/8Wry0uo.jpg) -->

### edges2shoes
#### edge -> shoes
| Input                                |                                      |                                      |
|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/cWWaOed.jpg) |                                      |                                      |
| Output                               |                                      |                                      |
| ![](https://i.imgur.com/kXYtgEV.jpg) | ![](https://i.imgur.com/sY68CE5.jpg) | ![](https://i.imgur.com/V6TffVp.jpg) |
| ![](https://i.imgur.com/53BHK6f.jpg) | ![](https://i.imgur.com/3C7UqJA.jpg) | ![](https://i.imgur.com/4XgaVOQ.jpg) |
| ![](https://i.imgur.com/sLNbEPb.jpg) | ![](https://i.imgur.com/V10aXI6.jpg) | ![](https://i.imgur.com/lKXm5kW.jpg) |
<!-- 
![](https://i.imgur.com/cWWaOed.jpg)![](https://i.imgur.com/kXYtgEV.jpg)
![](https://i.imgur.com/sY68CE5.jpg)![](https://i.imgur.com/V6TffVp.jpg)
![](https://i.imgur.com/53BHK6f.jpg)![](https://i.imgur.com/3C7UqJA.jpg)
![](https://i.imgur.com/4XgaVOQ.jpg)![](https://i.imgur.com/sLNbEPb.jpg)
![](https://i.imgur.com/V10aXI6.jpg)![](https://i.imgur.com/lKXm5kW.jpg) -->
#### shoe -> edges
| Input                                |                                      |                                      |
|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/Ccd45C4.jpg) |                                      |                                      |
| Output                               |                                      |                                      |
| ![](https://i.imgur.com/DdI2sfh.jpg) | ![](https://i.imgur.com/8F7cfBI.jpg) | ![](https://i.imgur.com/tnYgdT8.jpg) |
| ![](https://i.imgur.com/h4qFfqq.jpg) | ![](https://i.imgur.com/G3fSzg9.jpg) | ![](https://i.imgur.com/5Dc2By0.jpg) |
| ![](https://i.imgur.com/RZeUJb1.jpg) | ![](https://i.imgur.com/kKT7VAV.jpg) | ![](https://i.imgur.com/cs6KLtO.jpg) |

<!-- ![](https://i.imgur.com/Ccd45C4.jpg)![](https://i.imgur.com/DdI2sfh.jpg)
![](https://i.imgur.com/8F7cfBI.jpg)![](https://i.imgur.com/tnYgdT8.jpg)
![](https://i.imgur.com/h4qFfqq.jpg)![](https://i.imgur.com/G3fSzg9.jpg)
![](https://i.imgur.com/5Dc2By0.jpg)![](https://i.imgur.com/RZeUJb1.jpg)
![](https://i.imgur.com/kKT7VAV.jpg)![](https://i.imgur.com/cs6KLtO.jpg)
 -->
 
### bigcat2dog

#### bigcat -> dogs

| Input                                |                                      |                                      |
|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/fsmTxbR.jpg) |                                      |                                      |
| Output                               |                                      |                                      |
| ![](https://i.imgur.com/D4MC5Qr.jpg) | ![](https://i.imgur.com/MOfr3e5.jpg) | ![](https://i.imgur.com/7c51oMo.jpg) |
| ![](https://i.imgur.com/n6fXgwh.jpg) | ![](https://i.imgur.com/uA1IDPz.jpg) | ![](https://i.imgur.com/nmnv4CV.jpg) |
| ![](https://i.imgur.com/WAa71Rk.jpg) | ![](https://i.imgur.com/ZhNe2YN.jpg) | ![](https://i.imgur.com/ltrIibj.jpg) |

<!-- ![](https://i.imgur.com/fsmTxbR.jpg)
![](https://i.imgur.com/D4MC5Qr.jpg)![](https://i.imgur.com/MOfr3e5.jpg)
![](https://i.imgur.com/7c51oMo.jpg)![](https://i.imgur.com/n6fXgwh.jpg)
![](https://i.imgur.com/uA1IDPz.jpg)![](https://i.imgur.com/nmnv4CV.jpg)
![](https://i.imgur.com/WAa71Rk.jpg)
![](https://i.imgur.com/ZhNe2YN.jpg)![](https://i.imgur.com/ltrIibj.jpg) -->

#### dog -> bigcats
| Input                                 |                                      |                                      |
|---------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/aL6iABO.jpg)  |                                      |                                      |
| Output                                |                                      |                                      |
| ![](https://i.imgur.com/dWp7kG3.jpg)  | ![](https://i.imgur.com/hU3CQPP.jpg) | ![](https://i.imgur.com/u6EqPLX.jpg) |
| ![](https://i.imgur.com/j3EpmlR.jpg)  | ![](https://i.imgur.com/X1ZyCDX.jpg) | ![](https://i.imgur.com/Bjh0ybm.jpg) |
| ![](https://i.imgur.com/cgR8WA5.jpg)  | ![](https://i.imgur.com/URyA1tS.jpg) | ![](https://i.imgur.com/iOWrzei.jpg) |
<!--![](https://i.imgur.com/aL6iABO.jpg)
![](https://i.imgur.com/dWp7kG3.jpg)
![](https://i.imgur.com/hU3CQPP.jpg)
![](https://i.imgur.com/u6EqPLX.jpg)
![](https://i.imgur.com/j3EpmlR.jpg)
![](https://i.imgur.com/X1ZyCDX.jpg)
![](https://i.imgur.com/Bjh0ybm.jpg)
![](https://i.imgur.com/cgR8WA5.jpg)
![](https://i.imgur.com/URyA1tS.jpg)
![](https://i.imgur.com/iOWrzei.jpg)-->

### housecat2bigcat
#### housecat -> bigcats
| Input                                  |                                      |                                      |
|----------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/VxdUtYa.jpg)   |                                      |                                      |
| Output                                 |                                      |                                      |
| ![](https://i.imgur.com/8rG3SML.jpg)   | ![](https://i.imgur.com/7qn5kYy.jpg) | ![](https://i.imgur.com/XiYeb4k.jpg) |
| ![](https://i.imgur.com/3gtRGaU.jpg)   | ![](https://i.imgur.com/RKb07QA.jpg) | ![](https://i.imgur.com/gtlzPxz.jpg) |
| ![](https://i.imgur.com/9fzWnfE.jpg)   | ![](https://i.imgur.com/Xlc8Zyx.jpg) | ![](https://i.imgur.com/Mb4MshF.jpg) |
<!--![](https://i.imgur.com/VxdUtYa.jpg)
![](https://i.imgur.com/8rG3SML.jpg)![](https://i.imgur.com/7qn5kYy.jpg)
![](https://i.imgur.com/XiYeb4k.jpg)![](https://i.imgur.com/3gtRGaU.jpg)
![](https://i.imgur.com/RKb07QA.jpg)![](https://i.imgur.com/gtlzPxz.jpg)
![](https://i.imgur.com/9fzWnfE.jpg)
![](https://i.imgur.com/Xlc8Zyx.jpg)![](https://i.imgur.com/Mb4MshF.jpg)-->
#### bigcat -> housecats
| Input                                |                                      |                                      |
|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/YsidOho.jpg) |                                      |                                      |
| Output                               |                                      |                                      |
| ![](https://i.imgur.com/VWVBhKE.jpg) | ![](https://i.imgur.com/gknYYOb.jpg) | ![](https://i.imgur.com/ETvdHsm.jpg) |
| ![](https://i.imgur.com/kY882un.jpg) | ![](https://i.imgur.com/lTuYwQK.jpg) | ![](https://i.imgur.com/QhvEztD.jpg) |
| ![](https://i.imgur.com/tHHJbDP.jpg) | ![](https://i.imgur.com/Qaq7KP1.jpg) | ![](https://i.imgur.com/RRmYLLb.jpg) |
<!-- 
![](https://i.imgur.com/YsidOho.jpg)
![](https://i.imgur.com/VWVBhKE.jpg)![](https://i.imgur.com/gknYYOb.jpg)
![](https://i.imgur.com/ETvdHsm.jpg)
![](https://i.imgur.com/kY882un.jpg)![](https://i.imgur.com/lTuYwQK.jpg)
![](https://i.imgur.com/QhvEztD.jpg)![](https://i.imgur.com/tHHJbDP.jpg)
![](https://i.imgur.com/Qaq7KP1.jpg)![](https://i.imgur.com/RRmYLLb.jpg) -->

### housecat2dog
#### housecat -> dogs
| Input                                |                                      |                                      |
|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/XqBR9X5.jpg) |                                      |                                      |
| Output                               |                                      |                                      |
| ![](https://i.imgur.com/Jbgp4iR.jpg) | ![](https://i.imgur.com/QM3k7A5.jpg) | ![](https://i.imgur.com/JsUtmye.jpg) |
| ![](https://i.imgur.com/BCoMTVI.jpg) | ![](https://i.imgur.com/SIQzrf8.jpg) | ![](https://i.imgur.com/rrpJY7c.jpg) |
| ![](https://i.imgur.com/br2qfvJ.jpg) | ![](https://i.imgur.com/VGUy2YD.jpg) | ![](https://i.imgur.com/Eqf0O7W.jpg) |
<!--![](https://i.imgur.com/XqBR9X5.jpg)
![](https://i.imgur.com/Jbgp4iR.jpg)
![](https://i.imgur.com/QM3k7A5.jpg)
![](https://i.imgur.com/JsUtmye.jpg)
![](https://i.imgur.com/BCoMTVI.jpg)
![](https://i.imgur.com/SIQzrf8.jpg)
![](https://i.imgur.com/rrpJY7c.jpg)
![](https://i.imgur.com/br2qfvJ.jpg)
![](https://i.imgur.com/VGUy2YD.jpg)
![](https://i.imgur.com/Eqf0O7W.jpg)-->

#### dog -> housecats

| Input                                |                                      |                                      |
|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/hi483Ys.jpg) |                                      |                                      |
| Output                               |                                      |                                      |
| ![](https://i.imgur.com/ymEb96X.jpg) | ![](https://i.imgur.com/vh792kG.jpg) | ![](https://i.imgur.com/ZDYsvtE.jpg) |
| ![](https://i.imgur.com/DOJvyKh.jpg) | ![](https://i.imgur.com/aQtXgLT.jpg) | ![](https://i.imgur.com/LFk0iwu.jpg) |
| ![](https://i.imgur.com/9lRXDKi.jpg) | ![](https://i.imgur.com/myAqzwy.jpg) | ![](https://i.imgur.com/e0Ar5l6.jpg) |

<!-- ![](https://i.imgur.com/hi483Ys.jpg)
![](https://i.imgur.com/ymEb96X.jpg)
![](https://i.imgur.com/vh792kG.jpg)
![](https://i.imgur.com/ZDYsvtE.jpg)
![](https://i.imgur.com/DOJvyKh.jpg)
![](https://i.imgur.com/aQtXgLT.jpg)
![](https://i.imgur.com/LFk0iwu.jpg)
![](https://i.imgur.com/9lRXDKi.jpg)
![](https://i.imgur.com/myAqzwy.jpg)
![](https://i.imgur.com/e0Ar5l6.jpg) -->


## Conclusion

> 因為我們手上的 GPU 都在跑 ICCV 2019 的實驗，我們實在沒有足夠的運算資源再重新訓練 Reference 中的各個方法，所以我們只就他們展示出來的結果與方法比較。

### DRIT

![](https://i.imgur.com/Onmh6gw.png)

### Neural Style

![](https://i.imgur.com/c11rSAR.png)
![](https://i.imgur.com/p9JuF4S.jpg)

Results for PUBG trailer video:
scream style
![](https://i.imgur.com/a9rvQUB.jpg)
starry night style
![](https://i.imgur.com/rgOsnS5.jpg)

### Fast Photo Style

![](https://i.imgur.com/ZEAVqhb.jpg)

----


在效果上，只有 Fast Photo Sytle 與 DRIT 可以與 MUNIT 匹敵，他們產出跑夠真實的圖片，其中 MUNIT > Fast Photo Style > DRIT > Neural Style。而 Neural Style 這個古老（2015）的方法因為是使用 CNN 的各 layer 的特徵來做 transform，沒有將圖片轉換至共同的 latent space，所以對形狀的保留極差。

MUNIT 相較於其他方法的優勢在於他是一對多的。同一個 model，只要給定一張 image，就可以產出不同 domain 的轉換。這在實際應用上是較有前景的，例如藝術創作或產品設計。

----

在使用自己的圖片跑 MUNIT 動物之間轉換的 test 時，許多圖片的效果都不盡理想。臉的方向稍微有點角度就會使結果崩壞，在 test 的圖片上受到限制，因此我們都選用正臉的動物來達到最好的效果呈現。

在我們的實驗結果中，我們的 dog -> bigcat 和 housecat -> dog 較論文中效果不理想，在 test image 的選用上會大大影響實驗的結果。

在 neural style 的實驗中，我們有應用在 PUBG 的影片上，在第一個場景上的效果相當不錯；而第二個場景會有閃爍的現象，因為我們是做在每一個 frame 上，而 style transfer 的效果有機會作用在不同的位置而導致。

