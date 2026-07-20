# Learn_notes
===學習筆記本===
>先搞懂怎樣自架生圖套件，目前走的流派是Stable Diffusion+ComfyUI+Pony Diffusion V6 XL+LoRA   
>由於本人新手小白，所以如果有什麼看起來很蠢的操作請見諒   
**順便紀錄一下途中卡到的地方**
1. 需要NVIDIA CUDA支援   
*由於本身硬體效能較弱需要強化所以去安裝CUDA、TensorRT*   
   - CUDA安裝   
   不難，比較麻煩的是要依照作業系統環境、pythen版本、顯卡版本去下載適用的，要花點時間檢查一遍  
   - TensorRT安裝   
   這就有點難住我了，本人粗略了解過Pythen開發而已所以沒有試過在win系統安裝.whl  
   照著老黃的線上攻略本搞怎樣都安裝不了，結果發現是路徑問題「添加環境變數Path沒用」 
   
2. 開始安裝&設定ComfyUI   
   - 先安裝會用到的相依性套件，官方建議Nvidia使用者直接去pytorch下載   
   ```pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu130```   
   (新手小白估計會疑惑上面怎不會動，那是因為你可能沒有安裝python &要加上 -m )
   
   - 然後把ConfyUI會用到的依賴項目下載回來，官方有再下載包裡面放入requirements.txt這文件方便用指令處理   
   ```pip install -r requirements.txt```   
   (新手小白估計會又卡住，但原因估計跟上面一樣是路徑問題\"實際路徑+檔案含檔名\")   
   
   - 官方建議要安裝ComfyUI-manager，有這個就能手動調節節點，不用用命令列了   
   ```pip install -r manager_requirements.txt```   
   由於我們要使用的是Portable版本以及硬體比較弱，所以會使用run_nvidia_gpu_fast_fp16_accumulation.bat   
   開啟文字編輯器或者自己習慣的程式碼編輯器開啟，在第一行裡面追加以下參數   
   ```--enable-manager```
   
   - 很不幸的，嘗試運行失敗了，原因之一是因為我沒有安裝到ComfyUI_manager(該死的官方沒寫清楚)   
   請大家先到下面的[ComfyUI-Manager]下載主體，官方提供三種安裝方式，本人是用git clone   
   請先將CMD或者PowerShell的路徑CD到```你安裝的路徑```\ComfyUI\custom_nodes   
   ``` git clone https://github.com/ltdrdata/ComfyUI-Manager comfyui-manager ```   
   順便更新一下   
   ```python -m pip install -U comfyui-manager```   
   第二個原因是因為我的顯示卡驅動沒有跟上官方的最新版，更新一下就好了   
   
3. 接下來準備開始嘗試第一次生圖!開始學習怎樣控制與調整   
   - 先去找資料了解基本模型以及怎麼從一片空白中拉一個基礎的工作流程   
   雖然comfyui-wiki是建議我們去Civitai找模型，但是剛開頭一進去我就暈了   
   先不說分成兩個網站〔一般向〕or〔R18〕，裡面的模型風格太多而且大多是直接連同LoRA等工作流模組都掛再一起   
   雖然可以找一些願意提供免費的大神借他們調整好的，但是後面如果有要利用生成的作品去做分享與販售的話其實很不好   
   建議是直接下載未修改過的模型，可以先去Civitai看喜歡的風格，再去Hugging Face找原始模型   

   - 以下先把會弄到的主要幾個模型類型列出   
   1.checkpoint-主模型=影響產圖的主要風格與畫風，通常也是資料量最大的模型，最好參考自己的VRAM大小挑選   
   2.text_encoders-文本編碼模型=主要是配合一些小型文字AI去將提示詞先行轉譯成數字向量，能提升畫面描述精準度   
   3.clip-文本編碼模型=功能與text_encoders類似，不過其底層運作原理不同，此處更像是本字典能使用提示詞查找類似的作法   
     通常是與text_encoders一起使用強化精準描述   
   4.diffusion_models-擴散模型=實際動手幫你畫畫的畫家，不過通常是主模型兼職，不是必要模型，但是找好主模型時順便找一下以免有加補丁
   
5. 
   *其實如果硬體上資源夠的話可以一開始就用comfy-cli安裝跟調試就好了*   
   此處學習資源來自:   
   [ComfyUI安裝教學](https://ivonblog.com/posts/stable-diffusion-comfyui/)  
   [ComfyUI官方Github](https://github.com/Comfy-Org/ComfyUI)  
   [ComfyUI_Manager](https://github.com/Comfy-Org/ComfyUI-Manager)
