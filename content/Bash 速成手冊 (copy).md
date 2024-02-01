# Bash 速成手冊

這是一個專為想要快速掌握 Bash 命令列基本指令的新手使用者而設計的手冊。本手冊的目的是協助使用者快速熟悉 Bash 命令列環境，讓他們能夠迅速在命令列中進行工作。手冊重點介紹了 Bash 中的核心指令，包括但不限於 `cd`、`ls`、`cp`、`mv`、`rm` 等基本操作。這些指令是在命令列環境中進行日常工作時必須熟悉的基礎工具。雖然手冊未涵蓋所有指令的所有選項，但我們提供了基本的使用情境和示例。使用者可以根據自己的需要選擇性地查看指令的文件說明書 `man`，以深入了解各個指令的更多選項和用法。這本手冊也可以作為備忘錄使用。當您忘記某個指令的使用方式時，隨時可以回來查看相關內容。

## 目錄

<!-- TOC start (generated with https://github.com/derlin/bitdowntoc) -->

- [Bash 速成手冊](#bash-)
   * [目錄](#)
   * [命令列界面與圖形界面](#-1)
      + [提示符](#-2)
   * [基本指令](#-3)
      + [echo (印出文字)](#echo-)
      + [touch (新增一個空白檔案)](#touch-)
      + [ls (列出當前位置的目錄以及檔案)](#ls-)
      + [mkdir (新增資料夾)](#mkdir-)
      + [cd (切換目錄)](#cd-)
      + [pwd (確認當前的工作目錄)](#pwd-)
      + [mv (檔案移動)](#mv-)
      + [mv (改檔案名稱)](#mv--1)
      + [cp (複製檔案或目錄)](#cp-)
      + [rm (刪除檔案或目錄)](#rm-)
      + [history (歷史紀錄)](#history-)
      + [man (說明書)](#man-)
      + [Wildcard (萬用字元)](#wildcard-)
   * [熱鍵](#-4)
      + [Tab (自動補完)](#tab-)
      + [Ctrl + r (歷史搜尋)](#ctrl--r-)
      + [Ctrl + c (中斷程序)](#ctrl--c-)
   * [檔案權限](#-5)
      + [以 ls -l 檢視權限設定](#-ls--l-)
      + [chmod (改變檔案的權限)](#chmod-)
   * [資料檢視、修改、梳理](#-6)
      + [cat (顯示或連接文件的內容)](#cat-)
      + [less (以頁面的形式檢視文件)](#less-)
      + [head 和 tail (輸出文件的開頭或末尾的部分)](#head--tail-)
      + [wc (word count)](#wc-word-count)
      + [grep (搜尋文本)](#grep-)
      + [sort (排序)](#sort-)
      + [uniq (去除重複)](#uniq-)
      + [sed (取代)](#sed-)
   * [以 awk 處理表格資料](#-awk-)
   * [管線 ( | ) ](#---)
   * [檔案寫入](#-7)
      + [> (檔案寫入)](#-)
      + [>> (附加文字至最後一列)](#--1)
   * [Nano 文字編輯器](#nano-)
      + [Nano 的基本操作](#nano--1)

<!-- TOC end -->

## 命令列界面與圖形界面
**圖形界面 (GUI)** 是一種直觀的使用者介面，使用者可以透過滑鼠點擊和拖曳等視覺化手段完成各種任務，特別適合大眾使用者。相較之下，**命令列界面 (CLI)** 則是基於純文字的介面，雖然對習慣視覺化界面的使用者有一定學習曲線，但在高效性和靈活性方面優越。

舉例來說，在圖形界面中開啟一個文件需要多次點擊，而在命令列界面中，我們可以使用以下指令：

```bash
less /home/documents/holiday_files/food_list.txt
```

這個指令不僅迅速列出資料夾中所有文件，還可以直接讀取檔案內容。

進一步示範：想像手邊有一個資料夾，內含 1000 個檔案，需要在每個檔案名稱結尾加上`.abc`。在命令列界面中，我們可以用簡單的迴圈腳本完成，相比於手動改檔名更為高效。

```bash
for file in *; do mv "$file" "${file%.}.abc";done
```

這樣的操作不僅直觀高效，還可以透過腳本進行自動化處理，顯示了命令列界面在處理大量數據時的獨特優勢。

### 提示符

首先打開終端機 (Terminal) 後，你會看到以下範例文字，並且一個閃爍的游標等待你的輸入。

```bash
john@mycomputer:/home/user$
```

這是一段典型的 bash 在 Linux 系統上的預設提示符。以下是各個組件的解釋：

- 目前使用者, 這邊是的例子是 john
- 主機或系統名稱，以 `@主機名稱` 表示，這邊的例子是 `@mycomputer`
- 當前工作目錄位置，在檔案系統中的位置。在這邊的例子中 /home/john 意思是：跟目錄 (/) 下的 home 目錄裡面的使用者 john 目錄。
- $ 符號：這個符號表示提示符的結尾，通常用於一般使用者。

此外，在 Linux 系統中波浪符號 ~ 與 /home/user 同義。因此，你可能也會看到這種提示符。

```bash
john@mycomputer:~$
```

## 基本指令

以下是常用基本指令：

- `ls`: 列出 (list) 當前位置的目錄以及檔案。
- `cd`: 切換目錄 (change directory)。
- `mkdir`: 新增一個新的目錄 (make directory)。
- `cp`: 複製 (copy) 檔案或是目錄。
- `mv`: 移動 (move) 檔案或是目錄名稱，也可以更改檔案或是目錄名稱。
- `rm`: 刪除 (remove) 檔案或是目錄。
- `touch`: 新增一個空白檔案。
- `pwd`: 顯示當前工作目錄 (Present Working Directory)的路徑。

大多數的指令的語法如下:

- `指令 輸入檔案`
- `指令 輸入檔案 輸出檔案`
- `指令 [選項] 輸入檔案`
- `指令 [選項] 輸入檔案 輸出檔案`
    

現在，我們將透過以下範例來熟悉基本指令的使用方法和效果。首先，打開終端機（Terminal），您會看到提示符。系統顯示，您當前位於您的家目錄（/home/user）：
```bash
user@mycomputer:/home/user$
```

### echo (印出文字)

可將文字輸出到終端機或導入到檔案。
```bash
user@mycomputer:/home/user$ echo "Hello, World!"
Hello, World!
```

### touch (新增一個空白檔案)

讓我們新增一個空白檔案，名叫 tesfile。輸入以下指令，然後按 Enter 鍵：
```bash
user@mycomputer:/home/user$ touch testfile
user@mycomputer:/home/user$
```

### ls (列出當前位置的目錄以及檔案)

您會發現，除了出現新的提示符外，螢幕上似乎什麼事都沒發生。實際上，檔案已經建立完成。現在，使用 ls 指令來確認剛才新增的檔案：
```bash
user@mycomputer:/home/user$ ls
testfile
user@mycomputer:/home/user$ 
```
有些人的家目錄可能還會包含預設的資料夾或檔案，但我們暫時不需要理會它們。

### mkdir (新增資料夾)

現在，我們來學習新增一個資料夾，名稱為 testdir。輸入以下指令：
```bash
user@mycomputer:/home/user$ mkdir testdir
```
使用 `ls`  指令來確認剛才新增的資料夾。畫面輸出顯示剛才新增的資料夾和檔案：
```bash
user@mycomputer:/home/user$ ls
testdir  testfile
user@mycomputer:/home/user$ 
```

### cd (切換目錄)

現在，我們學習切換目錄，從家目錄切換到剛才新增的 testdir，輸入以下指令：
```bash
user@mycomputer:/home/user$ cd testdir
user@mycomputer:/home/user/testdir$
```
您會注意到提示符從 user@mycomputer:/home/user$ 變成 user@mycomputer:/home/user/testdir$

現在我們學習切換回上一層目錄。
```bash
user@mycomputer:/home/user/testdir$ cd ..
user@mycomputer:/home/user$
```
你會注意到提示符從 user@mycomputer:/home/user/testdir$ 變成 user@mycomputer:/home/user$

在 Liunx 系統中，兩個點 `..` 表示上一層目錄，而 一個點 `.` 表示當前目錄。

> ### 相對路徑與絕對路徑的
>
> 當目錄變得複雜後，使用*相對路徑*逐層切換目錄的方式確實有些繁瑣。因此，我們可以採用*絕對路徑*的方法，一次性到達目標目錄。請執行以下指令，並仔細觀察提示符的變化。請將 user 替換為您當前的使用者名稱：
>```bash
>user@mycomputer:/home/user/testdir$ cd /home/user
>user@mycomputer:/home/user$
>```
>我們可以發現，使用絕對路徑，不論身處何處，都能立即返回到家目錄。
>
>此外，在 Linux 系統中，波浪符號 `~` 與 `/home/user` 是等效的。因此，`cd ~` 等同於 `cd /home/user`。
>```bash
>user@mycomputer:/home/user/testdir$ cd ~
>user@mycomputer:/home/user$
>```
>
>絕對路徑和相對路徑是在檔案系統中用來指定檔案或目錄位置的兩種不同表示方式。相對路徑就像是口語中的走 3 號公路，在第 205 號交流道下去後，走第五大街；而絕對路徑則像是口語中的春田市第五大街 374 號。這兩者提供了不同的選擇，取決於您的需要和便利性。

### pwd (確認當前的工作目錄)

除了觀察提示符外，我們還可以使用指令 `pwd`（present working directory）來確認當前的工作目錄。
```bash
user@mycomputer:/home/user/testdir$ cd ~
user@mycomputer:/home/user$ pwd
/home/user
```

### mv (檔案移動)

現在我們將學習如何移動檔案，輸入以下指令：
```bash
user@mycomputer:/home/user$ cd ~
user@mycomputer:/home/user$ mv testfile ./testdir/
```
這個指令符合指令**輸入檔案 輸出檔案**的語法結構，即將 testfile 移動到 testdir 目錄下。執行後，如果使用 `ls ~ ` 指令，您會發現 testfile 已經不在家目錄中。然而，若使用 `ls ~/testdir` 指令，您會發現 testfile 出現在 testdir 目錄中。
```bash
user@mycomputer:/home/user$ ls
testdir
user@mycomputer:/home/user$ ls ./testdir
testfile
```
值得注意的是，這是一個展示 `ls` 結合相對路徑的應用，是一種*指令 輸入檔案*的語法。

### mv (改檔案名稱)

我們接著學習如何更改檔案名稱。
既然移動檔案的指令 `mv` 符合指令**輸入檔案 輸出檔案**的語法，那麼如果我們將檔案從目前工作目錄移動到同一目錄，並且指定新的檔案名稱，就能完成檔案更名了。輸入以下指令：
```bash
user@mycomputer:/home/user$ cd ~/testdir
user@mycomputer:/home/user/testdir$ mv testfile testfile_newname
user@mycomputer:/home/user/testdir$ ls
testfile_newname
```

### cp (複製檔案或目錄)

接著，我們學習複製檔案 `cp` 指令。這個指令的語法與 `mv` 一樣，都是指令**輸入檔案 輸出檔案**的語法結構。在這個示範中，我們以絕對路徑移動到 ~/testdir，然後創造一個空檔案，叫做 copied_file，然後再將這個檔案複製到上層目錄。最後以 `ls` 查看是否家目錄與 testdir 目錄裡面都有 copied_file。輸入以下指令：
```bash
user@mycomputer:/home/user$ cd ~/testdir
user@mycomputer:/home/user/testdir$ touch copied_file
user@mycomputer:/home/user/testdir$ cp copied_file ..
user@mycomputer:/home/user/testdir$ ls ..
copied_file  testdir
user@mycomputer:/home/user/testdir$ ls
copied_file  testfile_newname
```

### rm (刪除檔案或目錄)

我們學習使用 `rm` 指令刪除檔案。讓我們試著刪除家目錄的 copied_file 後，再利用 `ls` 查看是否家目錄的 copied_file 已經消失，而 ./testdir/ 內的 copied_file 還在。輸入以下指令：
```bash
user@mycomputer:/home/user/testdir$ cd ~
user@mycomputer:/home/user$ rm ./copied_file
user@mycomputer:/home/user$ ls
testdir 
user@mycomputer:/home/user$  ls ./testdir/
copied_file  testfile_newname
```

我們學習使用 `rm -r` 指令刪除整個 testdir 目錄。這是一個**指令 選項 輸入檔案**的語法，其中的 -r 選項代表遞迴 (recursive)，意思是要不斷地刪除目錄內的檔案，以及目錄本身。輸入以下指令：
```bash
user@mycomputer:/home/user/testdir$ cd ~
user@mycomputer:/home/user$ rm -r testdir
```
<span style="color:red;">請注意：在 Linux 系統中，rm 的刪除是不可逆的，而且檔案救援的成本非常高。</span>刪除的檔案不會出現在所謂的垃圾桶（或資源回收桶）。刪除就是刪除，系統不會給予任何警告。

### history (歷史紀錄)

`history` 指令用於顯示在命令列中執行過的指令歷史紀錄。這可以讓使用者輕鬆檢視並重複執行先前輸入過的指令。

範例:
```bash
user@mycomputer:/home/user$ history
1  ls
2  cd Documents/
3  nano file.txt
4  gcc program.c -o program
5  ./program
```
在這個例子中，history 顯示了最近執行的五個指令，每個指令前都有一個編號。使用者可以使用這些編號來重新執行特定的指令。

### man (說明書)

`man` 指令用於檢視與特定指令或主題相關的說明書。說明書提供了對指令、系統呼叫或文件的詳細說明，包括使用方法、選項、以及範例。很少有人能夠記住所有的指令，甚至包含指令的作者自己，因此我們使用 man 來查詢。

使用方式:
```bash
user@mycomputer:/home/user$ man ls
```

以下是部份輸出
```bash
LS(1)                           User Commands                          LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List information about the FILEs (the current directory by default).
       Sort entries alphabetically if none of -cftuvSUX nor --sort is
       specified.

       Mandatory  arguments  to  long  options are mandatory for short options
       too.  -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..

       -l     use a long listing format
...
```
在這個範例中，`ls` 指令的說明書顯示了 -l 選項的描述，該選項以長格式輸出目錄內容。這種格式提供了更詳細的檔案訊息，包括檔案類型、權限、擁有者、群組、檔案大小、修改時間等等。使用者可以透過閱讀說明書深入了解如何使用這些選項以及指令的其他功能。你可以使用箭頭鍵或滑鼠滾輪滾動頁面，按下 q 鍵退出說明書。

### Wildcard (萬用字元)

萬用字元星號`*`是在指令中使用的特殊字元，代表任意長度的字元。透過運用萬用字元，我們能夠更方便地處理多個檔案或目錄，使在命令列中執行諸如搜尋、複製、刪除等操作變得更加有效率。

範例 1: 輸入 `ls *.txt` 將列印出該工作目錄中所有副檔名為 .txt 的檔案。以下是一個範例指令，觀察不同的輸出。
```bash
user@mycomputer:/home/user$ touch abc.txt bcd.txt xyz.txt foo.png
user@mycomputer:/home/user$ ls
user@mycomputer:/home/user$ ls *.txt
abc.txt bcd.txt xyz.txt
user@mycomputer:/home/user$ ls *.png
foo.png
```

範例 2: 移動所有以 backup 開頭的檔案到 backup_folder
```bash
user@mycomputer:/home/user$ mkdir backup_folder
user@mycomputer:/home/user$ touch backup_a backup_b backup_c
user@mycomputer:/home/user$ mv backup* backup_folder/
user@mycomputer:/home/user$ ls backup_folder/
backup_a backup_b backup_c
```

範例 3: 刪除所有以 temp_ 開頭，且以 .txt 結尾的檔案
```bash
user@mycomputer:/home/user$ touch temp_a.txt temp_b.txt temp_c.txt temp_d.jpg
user@mycomputer:/home/user$ ls
touch temp_a.txt temp_b.txt temp_c.txt temp_d.jpg
user@mycomputer:/home/user$ rm temp_*.txt
user@mycomputer:/home/user$ ls
temp_d.jpg
```
範例 4: 複製所有檔案名稱中包含城市名稱與號碼，且結尾為 .txt 的檔案到 archived_dir
```bash
user@mycomputer:/home/user$ mkdir archieved_dir
user@mycomputer:/home/user$ touch file_city_NY_number_1.txt file_city_LA_number_323.txt file_city_Kansas_number_312.txt
user@mycomputer:/home/user$ cp file*city*number*.txt archieved_dir/
user@mycomputer:/home/user$ ls archieved_dir/
file_city_NY_number_1.txt file_city_LA_number_323.txt file_city_Kansas_number_312.txt
```
<span style="color:red;">注意: 在刪除檔案時請謹慎使用萬用字元！</span>請勿輕率執行類似 `rm -rf /*` 的指令，這樣的指令會強制刪除整個根目錄，也就是整個系統。雖然在大多數情況下使用者會因權限限制而失敗，但請絕不要隨便嘗試這樣的危險行為。

*恭喜，您已經學會了基本指令。這些指令足以應付大部分的工作。接下來，我們將學習進階指令，以提高工作效率。*

## 熱鍵

### Tab (自動補完)

透過按下 Tab 鍵，可以迅速完成輸入的指令或檔案名稱。當你開始輸入一個指令或檔案路徑，按下 Tab 鍵，系統會根據可用的選項自動完成輸入。這個功能非常重要，不僅節省時間，還能降低輸入錯誤的風險。

範例 1: 輸入 `tou` 後按一下 Tab 鍵，系統就會自動幫你補完指令為 `touch`

範例 2: 輸入 `ls /ho` 後按一下 Tab 鍵，系統就會自動幫你補完目錄為 `ls /home` 

範例 3: 輸入 `ls /home/user/fil` 後按一下 Tab 鍵，系統就會自動幫你補完檔案名稱為 `ls /home/user/file1.txt`

按兩下 Tab 鍵，畫面會印出其他可用的選項。例如
```bash
user@mycomputer:/home/user$ ls /home/  
# 按兩下 Tab 鍵，畫面會印出家目錄下其他使用者的目錄。
jhon  peter  alex jupiter
```
或是先輸入部份名稱後再按兩下 Tab 鍵，會出現與該名稱相關的可用指令、目錄、或檔案。
```bash
user@mycomputer:/home/user$ ls /home/j 
# 按兩下 Tab 鍵，畫面會印出家目錄下其他使用者的目錄以 j 開頭的選項。
jhon  jupiter
```

### Ctrl + r (歷史搜尋)

按下 `Ctrl + r` 後，開始輸入先前指令的一部分 (例如輸入：ls)，系統將搜索並顯示最相符的歷史指令 (在本例子是 `ls archieved_dir/`)。
```bash
(reverse-i-search)`ls': ls archieved_dir/
```

### Ctrl + c (中斷程序)

`Ctrl + c` 是一個鍵盤快捷鍵，用於中斷或停止當前正在執行的程序或指令，無論此時正在執行什麼操作。它的作用相當於強制停止按鈕，因此使用時應謹慎。此快捷鍵向正在執行的程序發送中斷信號，指示其立即停止執行。

請注意，有些程序可能需要處理中斷信號，並且可能不會立即停止。在某些情況下，`Ctrl + c` 可能無法中斷程序，這可能是因為程序處於無回應狀態。

以下是一個示範，這個指令會持續印出每秒一次的隨機數字，你可以按下 `Ctrl + c` 以中斷這個指令的執行。
```bash
user@mycomputer:/home/user$ while true; do echo $((RANDOM % 100)); sleep 1; do
```

## 檔案權限

### 以 ls -l 檢視權限設定

權限的設定不僅保護系統的安全性，同時防止系統被使用者未經授權修改造成不穩定或是重要資料外洩。我們可以使用 ls -l 來檢視權限設定。 在 `ls -l` 的輸出中，檔案的權限由 10 個字符組成 (例如： -rw-r--r--)，如下所示：
```bash
-rw-r--r-- 1 user group 1024 Jan 28 10:00 example.txt
```
這裡的第一個字符表示檔案的類型，一般檔案為 `-`, 資料夾則為 `d` 等等...。

接下來的九個字符則表示權限。這九個字符被分成三組，每組三個字符，分別代表擁有者、群組和其他使用者的權限。

- 擁有者權限 (Owner Permissions): 前三個字符表示擁有者對該檔案的權限，例如 rw- 表示擁有者有讀取（read）和寫入（write）權限，但沒有執行（execute）權限。

- 群組權限 (Group Permissions): 中間的三個字符表示與擁有者同群組的使用者對該檔案的權限。例如 r-- 表示群組成員只有讀取權限。

- 其他使用者權限 (Other User Permissions): 最後的三個字符表示其他使用者對該檔案的權限，不屬於擁有者或群組的使用者。例如 r-- 表示其他使用者只有讀取權限。

在 Linux 和 Unix 系統中，目錄也是一種檔案。因此目錄也需要不同權限的設定。以下是執行、讀取、寫入權限對於目錄的意義:

- 執行權限 (x): 進入目錄。為了能夠進入一個目錄，使用者必須擁有該目錄的執行權限。如果一個目錄沒有執行權限，即便使用者具有目錄內檔案的讀寫權限，也無法使用 `cd` 等指令進入該目錄。

- 讀取權限 (r): 查看目錄內容。讀取權限允許使用者列出目錄中的檔案和子目錄，也就是可以查看目錄的內容。如果目錄沒有讀取權限，使用者就無法查看目錄中的檔案列表，即便該使用者具有進入目錄的執行權限。

- 寫入權限 (w): 創建、刪除檔案和子目錄。寫入權限允許使用者在目錄中創建新的檔案或子目錄，同時也允許使用者刪除已存在的檔案或子目錄。如果目錄沒有寫入權限，使用者將無法在該目錄中執行 `touch` 創建檔案或 `mkdir` 創建子目錄等操作。

在多用戶環境下，遵守最小需要權限原則是確保安全性的重要一環。這意味著每個使用者只能獲得執行其工作所需的最低權限，而不是授予過多的權限，以減少潛在的風險。這種做法有助於降低誤操作、不當訪問或潛在的安全漏洞可能帶來的問題。


### chmod (改變檔案的權限)

在協作環境中，團隊成員通常需要共享和檢視檔案。因此，必須適度開放權限以讓團隊成員在需要時能夠讀取相關檔案。透過 `chmod` 指令，你可以根據需求更改檔案的權限，確保系統和檔案的安全性。

透過 chmod，你可以以數字形式或符號形式指定權限的變更。以下是 chmod 的基本語法：
```bash
user@mycomputer:/home/user$ chmod [選項] 模式 檔案
```

- 選項： 可以包含不同的選項，用於指定更多的設定。
- 模式： 可以使用數字形式或符號形式，來表示權限的變更。
- 檔案： 要修改權限的檔案名稱。

1. 使用數字形式修改權限:

- 4 表示讀取權限（read）
- 2 表示寫入權限（write）
- 1 表示執行權限（execute）

這三個權限的總和用數字表示，例如：

- 7 表示讀取、寫入和執行權限（4 + 2 + 1）。
- 6 表示讀取和寫入權限（4 + 2）。
- 5 表示讀取和執行權限（4 + 1）。

範例: 將檔案 example.txt 設置為擁有者具有讀取和寫入權限、群組具有讀取權限、其他使用者具有執行權限
```bash
user@mycomputer:/home/user$ chmod 764 example.txt
```

2. 使用符號形式修改權限:

- `+` 添加權限。
- `-` 移除權限。
- `=` 設置權限。

權限符號可以搭配 u（擁有者）、g（群組）、o（其他使用者）和 a（所有使用者）使用，以及 r, w, x 表示讀取、寫入、執行權限。

範例: 給檔案 script.sh 添加群組的執行權限:
```bash
user@mycomputer:/home/user$ chmod g+x script.sh
```
範例: 移除檔案 data.csv 中其他使用者的寫入權限:
```bash
user@mycomputer:/home/user$ chmod o-w data.csv
```

## 資料檢視、修改、梳理

在 Linux 或 Unix 系統中，有一些常用的指令用於檢視資料。一般來說，生物資訊檔都很大，大到一般家用電腦沒有足夠的記憶體開啟。這些指令能允許你在命令列環境下不需要將整個檔案載入記憶體的情況下檢視、修改、梳理資料。

以下是常見讀取資料的指令：

### cat (顯示或連接文件的內容)

`cat` 命令能將整個檔案的內容逐列輸出到終端機畫面，這在檢視小型的檔案很實用。但這在處理大型檔案時可能不是最佳方法。
```bash
user@mycomputer:/home/user$ cat filename.txt
```

### less (以頁面的形式檢視文件)

支援向前和向後滾動。這對於處理大型檔案很有用，因為它僅讀取顯示部分，而不是將整個檔案載入記憶體。按 q 退出。
```bash
user@mycomputer:/home/user$ less large_file.txt
```

### head 和 tail (輸出文件的開頭或末尾的部分)

`head` 和 `tail` 在檢視檔案結構或檢查檔案的最後幾列 (預設是 10 列) 時非常有用。
```bash
user@mycomputer:/home/user$ head large_file.txt
user@mycomputer:/home/user$ tail large_file.txt
```

### wc (word count)

這個命令輸出檔案的文字的列數、字串數、字元數。而無需將整個檔案載入記憶體。
```bash
user@mycomputer:/home/user$ wc .bashrc
145  588 4419 .bashrc
```

### grep (搜尋文本)

這個命令是搜尋和過濾文本。主要用來匹配文本列中的模式，然後列印匹配的列 (row)。
以下 grep 的基本使用方式和範例：

假設有一個檔案 example.txt 包含以下內容:
```
apple
banana
cherry
date
```
使用 grep 搜尋包含 "banana" 的列:
```bash
user@mycomputer:/home/user$ grep "banana" example.txt
banana
```

grep 還有各種選項跟支援標準表示式，譬如使用正規表示法搜尋以 "a" 結尾的單詞
```bash
grep "a$" example.txt
banana
cherry
```
>正規表示式（Regular Expression，簡稱 Regex 或 RegExp）是一種強大的字串匹配模式的描述工具。正規表示式由一系列的字符和特殊字符組成一個規則，該規則用於識別符合特定模式的字串。網路上已經有很多教學文章，而且每種語言中又有不同的擴充，本篇暫時先不講解。

### sort (排序)

這個命令是用於對文本文件進行排序操作。它可以按照字母順序 (預設)、數值大小等進行遞增或遞減排序。以下是範例:

按照字母順序排序: 假設有一個檔案 fruit_.txt 包含以下內容
```
banana
apple
grape
orange
```
使用 sort 按照字母順序排序:
```bash
user@mycomputer:/home/user$ sort fruit_.txt
apple
banana
grape
orange
```
使用 `-r` 選項可以執行反向排序:
```bash
user@mycomputer:/home/user$ sort -r fruit_.txt
orange
grape
banana
apple
```

按照數值大小排序: 假設有一個檔案 scores.txt 包含以下內容
```
2
5
10
25
```
使用 sort 按照數值大小排序:
```bash
user@mycomputer:/home/user$ sort -n scores.txt
2
5
10
25
```

### uniq (去除重複)

這個命令是用於去除或回傳相鄰且重複的列 (row)。以下是範例:

假設有一個已排序的檔案 sorted.txt 包含以下內容:
```
apple
apple
banana
grape
grape
orange
```

使用 `uniq` 刪除相鄰的重複列
```bash
user@mycomputer:/home/user$ uniq sorted.txt
apple
banana
grape
orange
```

使用 -c 選項可以顯示每列出現的次數:
```bash
user@mycomputer:/home/user$ uniq -c sorted.txt
2 apple
1 banana
2 grape
1 orange
```

使用 -d 選項可以僅顯示重複的列:
```bash
user@mycomputer:/home/user$ uniq -d sorted.txt
apple
grape
```

### sed (取代)

這個命令是用於對文本進行取代、刪除等等。語法是 `sed s///g`

以下是範例:

假設有一個檔案 example.txt 包含以下內容:
```
Hello, world!
This is a sample text.
```

使用 sed 將 "world" 替換為 "Ana":
```bash
user@mycomputer:/home/user$ sed 's/world/Ana/' example.txt
Hello, Ana!
This is a sample text.
```
使用 sed 將 "world" 替換為"空"的話，則為刪除:
```bash
user@mycomputer:/home/user$ sed 's/world//' example.txt
Hello, Ana!
This is a sample text.
```
若要整個文件都特換的話，加入 `g` 在結尾
```bash
user@mycomputer:/home/user$ sed 's/a/X/g' example.txt
Hello, world!
This is X sXmple text.
```
這裡是將文件中所有的 "a" 替換為 "X"

## 以 awk 處理表格資料

生物資訊檔案，有的以表格型態出現。例如: BED、GFF 格式等等。常常會有需要對每個欄位 (column) 做的需求。如同 excel 一樣，我們會有需要移動、調整欄位順序、輸入資料、篩選等等需求。在文字界面中可能沒有 excel 這種圖形界面的軟體。而且前面說過，這些生物資訊檔案通常都很大。在個人電腦中用 excel 開啟幾乎不太可能。因此，我們需要熟悉一個好用的表格工具 awk

awk 的基本語法，分三個區塊。
```
awk 'BEGIN {commands} pattern {commands} END {commands}' filename
```
BEGIN 區塊在處理開始前執行，可用於初始化變數或執行其他起始操作。
pattern 區塊用於指定條件，符合條件的列將執行後續的命令。
END 區塊在處理結束後執行，可用於輸出結果。

移動與調整欄位順序:

假設有一個 BED 格式的檔案 example.bed，內容如下:
```
chr1   100    200    gene1  50     +
chr2   300    400    gene2  22     -
```
我們想要將第四欄移到第一欄，可以使用以下 awk 命令:
```bash
user@mycomputer:/home/user$ awk '{print $4, $1, $2, $3, $5, $6}' example.bed
gene1 chr1 100 200 50 +
gene2 chr2 300 400 22 -
```
在這個範例中，我們省略了 BEGIN 與 pattern 區塊，直接執行 END 區塊。其中 $ 符號加上數字 n 用來表示第 1, 2, 3,..., n 欄位。此外 $0 表示列印全部欄位
```bash
user@mycomputer:/home/user$ awk '{print $0}' example.bed
chr1   100    200    gene1  50     +
chr2   300    400    gene2  22     -
```

列印部份欄位:
```bash
user@mycomputer:/home/user$ awk '{print $1, $2, $3, $4}' example.bed
chr1   100    200    gene1  50
chr2   300    400    gene2  22
```

篩選資料: 如果我們只想顯示某些列，可以使用 awk 的條件判斷。例如，只顯示第三欄 (基因名稱) 為 "gene1" 的列:
```bash
user@mycomputer:/home/user$ awk '$4 == "gene1" {print $0}' example.bed
chr1   100    200    gene1  50     +
```

計算總和: 如果我們想要計算第五欄的總和的話。
```bash
user@mycomputer:/home/user$  awk '{sum += $5} END { print "總和:", sum }' numbers.txt
總和: 72
```
在這個例子中，awk 會遍歷 numbers.txt 中的每一列，將每列的第 5 個欄位（使用 $5 表示）加總到 sum 變數中。最後，在處理結束 (END 區塊) 時，它會印出總和。
 
## 管線 ( | ) 

管線符號，稱為 pipe。這個符號允許將一個命令的輸出作為另一個命令的輸入，從而達成命令之間的連接。這種連接可以形成一個流水線，讓多個命令協同工作，完成更複雜的任務。以下是範例:

結合 `ls` 和 `grep` 命令，可以只要列印出有興趣的檔案。假設要列出當前目錄下以 ".txt" 結尾的檔案，可以使用以下命令:
```bash
ls | grep ".txt"
```
這裡，`ls` 顯示當前目錄下的所有檔案，然後將其輸出傳遞給 `grep` 然後過濾包含 ".txt" 的行，最終顯示符合條件的檔案。

使用 `sort` 和 `uniq` 排序並刪除重複列：
```bash
cat file.txt | sort | uniq
```
前面提過，使用 `unqi` 指令前，檔案內容建議先排序過。因此，這裡先使用 `cat file.txt` 顯示文件的內容，然後將其輸出傳遞給 `sort`，再將排序後的輸出傳遞給 `uniq`，最終得到排序並刪除重複列的結果。

管線最主要的功能就是處理資料流。這是一種將文本作為連續位元流 (byte stream) 逐個處理的概念。這種處理方式是一種逐列、逐字節或逐字符的過程，文本的處理不需要一次性將整個檔案讀取到記憶體中，而是透過資料流的方式依次處理。這對於處理大型文本檔案非常有利。有了資料流，我們就不需要把資料處理過程中的半成品資訊暫存在記替體或是輸出成一個檔案，然後再輸入之類的繁瑣行為。

## 檔案寫入

學會讀取檔案後，我們學著寫入檔案


### > (檔案寫入)

可以將命令輸出的內容導入至檔案。如果檔案不存在，則會建立一個新的檔案；<span style="color:red;"> 如果檔案已存在，則會覆蓋原有檔案的內容。</span>
```bash
echo "Hello, File!" > output.txt
```

### >> (附加文字至最後一列)

附加符號用於將命令的輸出追加到現有檔案的末尾，而不是覆蓋原有內容。試著執行以下範例，並且觀察輸出。
```bash
user@mycomputer:/home/user$ echo "This is row 1" > output.txt
user@mycomputer:/home/user$ cat output.txt
This is row 1
user@mycomputer:/home/user$ echo "This is row 2" >> output.txt
user@mycomputer:/home/user$ cat output.txt
This is row 1
This is row 2
```

## Nano 文字編輯器

上篇介紹的檔案寫入，在自動化腳本裡面有非常重要的地位。但是在大量文字編輯時，效率仍然不足。這時候我們需要文字編輯器。Nano 是一個輕量且易於使用的文字編輯器，常用於終端機或命令列介面，具有基本的文字編輯功能，並且對於新手而言相對容易上手。以下是一些 Nano 編輯器的基本介紹和使用示例: 

### Nano 的基本操作

使用 `nano` 指令，並指定要編輯的檔案名稱。如果檔案不存在，Nano 將創建一個新的檔案。
```bash
nano filename.txt
```

基本快捷鍵：

- 使用箭頭鍵移動光標。
- Ctrl + G：顯示說明文件（Help）。
- Ctrl + X：離開 Nano，如果有修改，將提示是否儲存。
- Ctrl + O：儲存當前檔案。
- Ctrl + W：尋找文字。
- Ctrl + K：剪下（刪除）一行。
- Ctrl + U：貼上被剪下的文字。

Nano 的簡單操作和快捷鍵使得它成為初學者或只需要進行基本文字編輯的使用者的理想選擇。不過，對於更複雜的編輯需求，可能需要使用更強大的文字編輯器，如 Vim 或 Emacs