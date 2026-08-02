# ComfyUi學習筆記本 #  
### 前言 ###  
>這是我剛接觸AI相關學習的第一站，所以當中可能會有不少錯漏或者觀念不正確的部分  
>還有我學習的方式是先從如何應用在生活當中再往如何建置自動工作流，不是正規的做法所以不用太奇怪  
>由於剛剛接觸python開發環境，所以可能會走些歪路，看到就麻煩提醒指導了
  
### 配置開發環境-工欲善其事，必先利其器 ###  
*既然是要自主學習必須至少把應有的開發環境先配置好，基本上可以參考微軟或者AWS的機器學習環境配置*  
- python =>建議最好不要直接使用最新版本，可以依照最新版本往前推至少兩次版本號，通常最新版大家還沒跟上發布修改  
- PyTorch =>很多AI文字推論、深度學習、微調等相關功能都會需要用到，安裝時請注意支援的python版本  
- CUDA =>我有Nvidia GPU顯示卡所以才裝這個，一定安裝最新版同時把自己的顯示卡驅動更新最新版本  
- TensorFlow =>如果你有Nvidia GPU，可以安裝這個強化你的AI去調用CUDA GPU  
- TensorRT =>有安裝上面那個自然會需要這個，可以加快模型的運轉效率，不過其實不是標配要或不要視個人需求  
  
### 開始安裝-全新的開始 ###
*加入過程一些需要注意的小狀況*  
- 首先官方 [ComfyUI_github](https://github.com/Comfy-Org/ComfyUI) 有給Windows Portable Package的下載包可以直接下載下來放到指定的資料夾即可後續使用  
但是想要安穩的吃到電腦上的硬體資源建議用手動作法  
- 建議使用comfy-cli，安裝後可以直接使用命令下載主體檔案包含ComfyUI-Manager等所有相關的套件  
``` python -m pip install comfy-cli ```  
``` comfy install ```  
- 或者不想要安裝太多多餘的套件可以使用只安裝主體這條路  
  *下載前記得先把終端機路徑切換到你想安裝的資料夾去*  
  以下是配合我剛好有Nvidia GPU所下的指令
  ``` git clone https://github.com/ComfyUI ```
  然後安裝本體的依賴項與更新  
  ``` python pip install -r requirements.txt ```
  進入安裝的資料夾當中找到update資料夾，點選update_comfyui.bat更新  
  此時主體當中未包含ComfyUI-Manager，需要自行到[ComfyUI_Manager](https://github.com/Comfy-Org/ComfyUI-Manager)下載  
  ``` git clone https://github.com/ltdrdata/ComfyUI-Manager comfyui-manager ```  
  ``` python pip install -r manager_requirements.txt ```  
  這樣就能使用run_cpu.bat啟動你的comfyui了
  
### 理解運作邏輯以及實際操作 ###  
*首先來個網路上找的流程圖*【如有版權問題請留信告知我把它刪除】  
<img width="768" height="381" alt="image" src="https://github.com/user-attachments/assets/ea4bf2e0-d737-4fcc-813f-2852b39b9ade" />  
我對於流程圖的理解  
Pixel Space(像素圖空間)此處原始圖片需要經由VAE Encode(變分編碼器)編碼成向量數並壓縮放入Latent Space(潛在空間)  
然後經由Diffusion Process(擴散噪點)將在潛在空間的向量數加入噪點使其失去原始樣態  
以機器學習角度來看比較像是故意加入額外的向量數把權重打亂...吧?  
右側的Conditioning(訓練條件)是要混合的材料，如語意地圖（Semantic Map）、文字（Text）、結構表徵（Representations）或圖像（Images)，
材料經由文字編碼器(text_encoders)、Embedding(語意)、LoRA(結構表徵)等等轉換成向量數【T0的部分】  
之後將外部輸入的向量數混入本來在潛在空間中的原始圖向量數並使用Denoising U-Net(網格去噪)依步數設定疊代去噪過程  
疊代過程中模型會慢慢的將外部的物件與原始圖的物件做融合使其盡量自然，最後再經由VAE Decode將向量數據反向解碼成圖
  
*理解名詞*  
- 使用工具的第一步就是先了解UI與UX，試著去操作介面上的功能以及用途  
1.   
  
*理解節點*  
- 將各節點的主要功能都摸過一次，實際測試文生圖流程以及官方所提到的基礎工作流每個節點各自會對最終成品造成什麼影響  
1. Checkpoint[load checkpoint]=>  
2. CLIP[CLIP Text Encode]=>  
3. Latent[Empty Latent Image]=>   
4. KSampler=>  
5. VAE[VAE Decode]=>
6. Save Image=>

  
