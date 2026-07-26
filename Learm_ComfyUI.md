# ComfyUi學習筆記本 #  
1. 前言  
** 這是我剛接觸AI相關學習的第一站，所以當中可能會有不少錯漏或者觀念不正確的部分  **
** 還有我學習的方式是先從如何應用在生活當中再往如何建置自動工作流，所以如果是想參考如何商用的可能會失望了  **

2. 配置開發環境-工欲善其事，必先利其器  
** 既然是要自主學習必須至少把應有的開發環境先配置好，基本上可以參考微軟或者AWS的機器學習環境配置  **
  
- python =>建議最好不要直接使用最新版本，可以依照最新版本往前推至少兩次版本號，通常最新版大家還沒跟上發布修改  
- PyTorch =>很多AI文字推論、深度學習、微調等相關功能都會需要用到，安裝時請注意支援的python版本  
- CUDA =>我有Nvidia GPU顯示卡所以才裝這個，一定安裝最新版同時把自己的顯示卡驅動更新最新版本  
- TensorFlow =>如果你有Nvidia GPU，可以安裝這個強化你的AI去調用CUDA GPU  
- TensorRT =>有安裝上面那個自然會需要這個，可以加快模型的運轉效率，不過其實不是標配要或不要視個人需求  

3. 開始安裝-全新的開始
** 會加入過程一些需要注意的小狀況  **
- 首先官方 [ComfyUI_github](https://github.com/Comfy-Org/ComfyUI) 有給Windows Portable Package的下載包可以直接下載下來放到指定的資料夾即可後續使用
但是想要安穩的吃到電腦上的硬體資源建議用手動作法  
- 建議使用comfy-cli，安裝後可以直接使用命令下載主體檔案包含ComfyUI-Manager等所有相關的套件  
``` python -m pip install comfy-cli ```  
``` comfy install ```  
- 或者不想要安裝太多多餘的套件可以使用只安裝主體這條路，以下是配合我的Nvidia GPU的指令  
```git clone https://github.com/ComfyUI ```  
小提醒，下載前記得先把終端機路徑切換到你想安裝的資料夾去  
- 然後安裝本體的依賴項與更新  
``` python -m pip install -r requirements.txt ```
進入安裝的資料夾當中找到update資料夾，點選update_comfyui.bat更新，這樣就能使用run_cpu.bat啟動你的comfyui了
小提醒，此時主體當中未包含ComfyUI-Manager，需要自行到[ComfyUI_Manager](https://github.com/Comfy-Org/ComfyUI-Manager)下載
``` git clone https://github.com/ltdrdata/ComfyUI-Manager comfyui-manager ```  

4. 開始嘗試理解運作邏輯
