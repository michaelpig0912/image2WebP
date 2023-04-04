# 使用 Python 快速輕鬆地將 HEIC、JPG、PNG 轉換為 WebP
當我們在製作網頁時，通常需要大量的圖片，但是網頁的載入速度會因為圖片的大小而變慢，進而導致SEO的分數變差。WebP是一種由Google推出的圖片格式，可以有效地減小圖片的大小，同時也保持了圖片的品質。在這篇文章中，我們會使用Python來將HEIC、JPG、JPEG和PNG格式的照片轉換成WebP格式，並且移除其中的照片資訊，以保護個人隱私。

## 安裝依賴庫
Pillow是一個Python圖像處理庫，而pillow-heif是一個Pillow套件，可以處理HEIF格式的圖片。要使用這個套件，請在命令行中輸入以下指令：
```bash
pip install pillow pillow-heif
```
## 程式
這個程式會先從指定的目錄中，尋找HEIC、JPG、JPEG和PNG格式的照片，並且使用Pillow來將它們轉換成WebP格式。
也會同時移除照片中的EXIF資訊。

這個程式的主要要達到的功能有三個：

1. 想要將 HEIC、JPG、JPEG 轉換為 WebP ，並且解析度不更改，檔名也維持一樣。
2. 將想要轉換的 HEIC、JPG、JPEG 檔案放在與程式相同位置的 `/image` 資料夾下，並且輸出的檔案在同一資料夾內。
3. 移除其中的EXIF資訊。

接下來是程式碼的說明，
1. 程式的主要流程是使用`os.walk`函數遍歷圖片資料夾中的所有檔案，判斷檔案類型是否為heic、jpg、jpeg或png，如果是就呼叫convert_to_webp函數進行轉換。
2. `convert_to_webp`函數中，我們首先使用Pillow套件的`Image.open`函數讀取圖片檔案，然後將其轉換為RGB模式，因為webp不支援其他模式的圖片。
3. 接著，我們使用`Image.getexif`函數獲取圖片的exif資訊，如果有EXIF資訊，則轉換為bytes類型，否則為空bytes。
4. 最後，我們使用`Image.save`函數將轉換後的圖片儲存為webp格式，設置品質為80，並移除exif資訊。
5. 如果轉換成功，就輸出成功訊息，否則輸出錯誤訊息。
6. 最後加上判斷程式是否作為主程式執行的判斷，如果是，就呼叫`main`函數，這樣在執行這個程式的時候，就可以自動遍歷指定的資料夾，並轉換所有符合條件的圖片檔案了。

## 運行程式
要使用此程式，請按照以下步驟操作：

1. 確保已經安裝了 Python 以及 Pillow 和 pillow-heif 。
2. 將上述程式儲存為名為 `convert_to_webp.py`。
3. 在程式所在的目錄下創建一個名為 image 的文件夾，將想要轉換的圖片放入該文件夾中。
4. 打開命令列 ( CMD )，進入至程式所在的目錄，然後運行以下命令：
```bash
python heic_to_jpg.py
```
5. 程式將自動尋找` /image `文件夾中的所有圖片，並將其轉換為 WebP 。
6. 轉換後的 WebP 文件將與原來的 HEIC 圖片的相同的文件夾中。
