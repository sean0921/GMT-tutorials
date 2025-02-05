======================================
基本概念與名詞
======================================

GMT 繼承了在 UNIX 環境之下處理資料的方法，對於曾經接觸過 shell 或 cmd 的人，它的操作方法應該不陌生。如果你之前完全沒有用過，也沒有關係，以下將提供一些必要的基本概念，稍微熟悉後，就可以快速上手。

另外，這裡也會簡單介紹 GMT 相關的一些檔案格式與操作，如果你是第一次接觸地理空間的資料，也歡迎在此查閱相關的術語。

UNIX 環境
--------------------------------------

.. _Terminal:
.. _終端機:

終端機
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
雖然目前主要的作業系統都是以圖形介面 (桌面) 當作預設的使用者介面，但是你仍然可以透過指令列來控制你的電腦。最簡單的方法就是透過作業系統在桌面環境下內建的指令列程式來執行。指令列程式在 Windows 下稱為 cmd，而 Mac 或大部分 Linux 系統則稱為終端機 (terminal)。在本教學中，「開啟終端機」就意味開啟指令列模式來操作你的電腦。在 Windows XP 之後的版本，有兩種「終端機」可以選擇，一個就是 cmd，另一個稱為「PowerShell」，簡單的說就是讓使用者可以在 Windows 的介面之下使用 UNIX 殼程式 (shell) 的一些語法。在本教學中，所有要在終端機下輸入的指令，最前方都會有個提示符號

.. code-block:: bash

    $

接在 ``$`` 之後的文字，才是使用者真正要輸入的指令。有關如何開啟作業系統的指令模式，請參考相關的專書或網頁，於此不再贅述。

殼層 (Shell)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
簡單的說來，殼層指的是使用者和「電腦這台機器」進行互動的介面，像是 Windows 的桌面環境、或是某個作業系統的指令列程式，都稱之為殼層。不同的殼層有不同的與電腦互動的方法，例如在文字介面殼層中，使用者要下達預先定義的指令，才能命令電腦做事。最初的 GMT 使用者介面，就是建立在一個很有名的、指令列程式型的殼層之中，它叫做 **sh**。經過了長時間的發展，GMT 已經被移植到了不同作業系統下的指令列殼層，例如說 Windows 的 cmd，但是 GMT 的指令語法仍然維持著原本殼層的格式。基本上，你可以把這些格式直接視作 GMT 指令操作的一部分來學習。有關於殼層的基本語法，許多資訊科學的專書或網頁均有詳細介紹，例如\ `鳥哥的Linux 私房菜 <http://linux.vbird.org/>`_。會一點殼層的指令，絕對對操作 GMT 有莫大的助益。

.. tip::

    有一個語法倒是非常值得一記，那就是註解符號 ``#``，例如以下指令：

    .. code-block:: bash

        $ gmt grdinfo 你的檔案.grd     # 觀看檔案的資訊

    在 ``#`` 後面的文字，是對指令的補充說明。本教學中，也會使用此格式，使腳本更易於閱讀。

.. _Script:
.. _腳本:

批次檔或腳本
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在指令列程式中，每按下一次 ``Enter`` 鍵，就會立刻執行當下的指令。但使用者也可以選擇把所有想要執行的程式統一寫在一個純文字檔中，然後在指令列程式輸入檔名，電腦就會逐一讀取文字檔中的指令並執行。在 Windows 中，這種檔案叫做「批次檔 (batch file)」，而在 sh 或由它衍生的各種殼層中，通常會稱為「腳本 (script)」，但基本上他們指的是同一件東西，在本教學中，將統一稱之為「腳本」。不同系統在執行腳本的操作細節上，會有些許差異，而且通常也有許多種方式可以讀取腳本。以下是筆者推薦的操作方法。

- Windows: 把 ``.txt`` 腳本檔案的副檔名改成 ``.bat``，然後點兩下此檔，Windows 就會自動開啟 cmd 來執行。一般來說，腳本的最後一行可以放上

  .. code-block:: bash

    ...(以上都是你的指令)
    pause

  加上 ``pause`` 之後，腳本執行完不會直接關閉 cmd 視窗，你可以在手動關閉前，先看一下所有指令的執行情況。

- Unix 為基礎的系統 (Linux 或 Mac 等等): 副檔名可以隨便命名，筆者通常偏好以 ``.sh``、``.csh`` 或 ``.bash`` 結尾，端看你想要用哪種殼程式進行操作。以 bash 為例，腳本的第一行可以放上

  .. code-block:: bash

    #!/bin/bash
    ...(以下都是你的指令)

  然後在指令列中，改變檔案權限

  .. code-block:: bash

    $ chmod +x 你的腳本.bash

  這樣要執行時，就可以直接下達如下指令，非常方便：

  .. code-block:: bash

    $ 你的腳本路徑/你的腳本.bash

在本教學中，\ **所有的 GMT 腳本都是以 bash 語法編寫**\ 。雖然不管你使用的是哪種作業系統或殼程式，GMT 的指令都會相同，但是因為腳本中難免會出現隨著殼程式不同而變化的語法，因此如果你使用的是除了 bash 之外的其他殼 (csh、tcsh、cmd、Power Shell 等等)，本教學的腳本在執行之前，可能需要小幅的修改成符合你使用的殼的語法，尤其是像指定變數、迴圈、建立檔案、文字資料處理等等的操作。

至於在本教學中出現的 PyGMT 腳本...當然就是以 `Python`_ 語言撰寫的啦！

.. 在本教學中，腳本的格式預設以 Linux 或 Mac 為主。也就是說，Windows 使用者可以把本教學中
   出現的腳本內的 ``#!/bin/bash`` 移除，不會影響輸出。實際上，就算不移除此行，Windows 
   也會把它當成是註解而直接略過，所以本教學的腳本程式碼，應可適用於各作業系統。

地理空間資料
--------------------------------------

NetCDF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
NetCDF 是 Network Common Data Form 的縮寫，直譯為「網路通用數據格式」。顧名思義，他是一種儲存資料的格式，由 UCAR (美國大氣研究大學聯盟) 在 1989 年開始設計、發展到現在。NetCDF 最初的目標，是要為科學資料提供一種統一的儲存格式，以方便研究人員互相傳遞資料。除了設計儲存格式外，UCAR 也為 netCDF 編寫了一系列的模組與函數庫，讓使用者可以簡單的在各種程式語言或環境中操作這些資料。NetCDF 是 GMT 主要支援的檔案格式，常見的附檔名為 ``.nc``，不過有時也會用 ``.grd`` 副檔名，來表示它的資料結構。它以二進位模式儲存資料，而且除了資料數據本身外，也附有檔頭描述這些數據的基本資訊 (這些檔頭通常稱為「中繼資料」，英文是 Metadata)。NetCDF 還有一個特點，就是它的資料跟作業系統的\ `位元儲存序 <https://zh.wikipedia.org/wiki/%E5%AD%97%E8%8A%82%E5%BA%8F>`_\ 無關，使用者不須擔心資料傳給別人後會讀取錯誤。其他詳細的說明，請參閱 `netCDF 網站 <http://www.unidata.ucar.edu/software/netcdf/>`_。

大地座標系統 (Datum)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
大地座標系統，就是一批用以描述地球形狀的參數，以及運用這些參數計算出來的地球表面的三維座標。目前全世界最通用的大地座標系統為 **WGS84** (又稱之為 **EPSG:4326**)，它也是 GPS 衛星所採用的大地座標系統。

以 WGS84 為例，它把地球的形狀定義成兩極略扁的橢球，橢球的中心對準地球的質心。這個形狀通常稱為 **WGS84 參考橢球**。此外在地表的水平座標設定上，緯度原點是赤道大圓，經度子午線原點則稍稍偏離了格林威治天文台。

簡而言之，大地座標系統就是一整套幫地表設定三維座標 **(經度，緯度，高度)** 的參數集合。GMT 預設的大地座標系統也是 WGS84，你也可以使用以下指令查看現在 GMT 的座標系統：

  .. code-block:: bash

    $ gmt defaults -D   # 在 Projection Parameters 的欄位



而關於地表的垂直高度，WGS84 表示的數值則是與\ `大地水準面 <https://zh.wikipedia.org/wiki/%E5%A4%A7%E5%9C%B0%E6%B0%B4%E5%87%86%E9%9D%A2>`_\ 的差距。目前 WGS84 使用 **EGM96** 這個地球的重力模型來設定地球的大地水準面。

.. attention::

    大地座標系統基本上是不會定義垂直高度的參考基準的，它必須要由使用者自己決定。目前常用的基準有兩個：

    1. 直接用參考橢球的表面當基準測量高度，稱之為\ **橢球高**。
    2. 使用海水面 
       (`大地水準面 <https://zh.wikipedia.org/wiki/%E5%A4%A7%E5%9C%B0%E6%B0%B4%E5%87%86%E9%9D%A2>`_\) 
       當基準測量高度，稱之為\ **正高**。目前常用的標準為 **EGM96** 這個地球的重力模型。

    慣例上，以 WGS84 做基準的資料都會採用\ **正高**\ 來表示高度，但並非所有的資料都會遵循這條規則。如果你對高度有精細的要求，例如誤差須在數十公尺內，最好確認一下你的資料是使用哪種高度參考基準。

投影法與投影座標系統 (Projected Coordinate System)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
由於大部分的地圖都是平面的，再加上我們畫區域性的地圖時，經緯度也沒那麼方便 (1 度是 100 多公里，如果地圖很小，常常都只會有幾弧分或幾弧秒的改變)，所以在許多時候，我們會使用特定的投影法，把地球的弧面依照某種幾何公式拓展成平面，這樣地圖上一個點的座標，就可以用 **(二維 X 座標，二維 Y 座標，高度)** 來表示。這種座標表示法，就稱作投影座標系統。

要創造投影座標系統，必須要指定地球的形狀 (也就是大地座標系統中的參考橢球) 和投影法。目前全球最通用的投影座標系統稱為 **UTM**，是 Universal Transverse Mercator 的縮寫，中文為「全球橫麥卡托投影」。它使用 WGS84 的參考橢球，把地球切割成許多區域，每個區域個別使用\ `橫麥卡托投影法 <https://en.wikipedia.org/wiki/Transverse_Mercator_projection>`_\ 來製作地圖的二維座標。

如果想要知道更多有關投影法的細節與不同投影法和投影座標系統的介紹，可以參考\ `臺師大的地圖投影解說 <http://hep.ccic.ntnu.edu.tw/browse2.php?s=237>`_\ 或\ `上河文化的解說網頁 <http://www.sunriver.com.tw/grid_tm2.htm>`_。

.. note::

    除了 WGS84 外，台灣還有兩個常用的大地座標系統，稱為 **TWD67** 與 **TWD97**，與之對應的投影座標系統則是 TWD67-TM2 與 TWD97-TM2。這兩個大地座標系統設定的地球橢球體外型，都跟 WGS84 不一樣，其中 TWD67 的差距較大，導致算出來的座標會與 WGS84 有數百公尺至一公里的差距；而 TWD97 就非常的接近 WGS84，在台灣地區的座標差距大致上只有數十公分。\ [1]_

GMT 6 的新語法模式
--------------------------------------
在 2019 年秋季釋出的 GMT 6 是目前最新的 GMT 版本，也是本手冊內文指令使用的版本。製作團隊在此版本中，引進了一個全新的語法系統，稱為現代模式 (Modern Mode)，以和 GMT 第五版與之前的傳統模式 (Classic Mode) 區別。在現代模式中，GMT 把 PostScript 的繪圖步驟轉移到暫存檔中，並直接產生向量形式的 PDF 或是影像形式的 PNG 與 JPG，因此大大簡化了腳本的繁雜程度。以下列出現代模式和傳統模式最主要的差別\ [2]_\ ：

- GMT 指令不再透過 UNIX 的輸出重導向 (``>``) 把地圖存到 ``.ps`` 檔中。
- 使用者不用再透過 ``-O`` 與 ``-K`` 選項「連接」不同的 GMT 指令。
- 因為可以直接選擇多種出圖格式，使用者不用再花費時間轉檔。
- 出圖的版面尺寸不再綁定紙張尺寸，而是會自動裁切到繪圖區域的大小。因此，``-P`` 選項也不需要了。
- 許多 ``ps`` 開頭的指令改了名字，多半是把 ``ps`` 刪掉，但也有完全改掉的例子，例如 ``psxy`` 變成了 ``plot``。
- 在現代模式中，使用者\ **必須**\ 要透過 ``gmt begin`` 與 ``gmt end`` 來包住繪圖的指令。在傳統模式中無此語法。
- 重複的繪圖區域 ``-R`` 和投影 ``-J`` 等設定，再也不用在每一個指令中都列出。
- 增加了 ``subplot`` 指令，讓製作多合一地圖變得很容易。

為了向下相容使用舊版語法的腳本，在 GMT 6 中你可以使用現代模式或是傳統模式的語法。因為新的語法具有許多優點，\ **在本教學手冊中，我會使用現代模式的語法來撰寫腳本**\ 。然而，在部份繪製地圖的章節中，我也會一併放上傳統模式的教學連結以及使用傳統模式撰寫的腳本，供各位使用者參考。

如果你已經是 GMT 5 的使用者，可以馬上無痛升級到 GMT 6，因為幾乎所有第五版的語法在第六版中都有支援 (傳統模式)。

如果你已經是 GMT 4 的使用者，以下列出幾個例子顯示 GMT 6 (傳統模式) 與 GMT 4 指令上的不同：

    .. code-block:: bash

        $ pscoast 各種選項...       # GMT 4 的 pscoast 指令
        $ gmt coast 各種選項...     # 在 GMT 6 中，換成了 coast 指令，而且變成總指令 gmt 下屬的一個模組。
	$ gmtset 各種選項...        # GMT 4 的 gmtset 指令
        $ gmt set 各種選項...       # 在 GMT 6 中也換成了 set 指令，而且變成總指令 gmt 下屬的一個模組。

然而，在安裝 GMT 6 的時候，系統會問你要不要替所有 ``gmt`` 指令下屬的模組建立捷徑。如果你選了 Yes，那麼你就可以使用 GMT 4 的語法來讓 GMT 6 執行你的腳本 (意思就是，GMT 會讓系統理解 ``pscoast`` 等等 GMT 的舊指令名字)。


.. 在 2013 年秋季釋出的 GMT 5 是目前最新的 GMT 版本\ [2]_\ ，也是本手冊內文指令使用的版本。這個版本最主要的更動，是把所有的 GMT 指令濃縮到了一個指令：\ ``gmt``\ 。以常用的指令 ``pscoast`` 與 ``gmtset`` 為例，GMT 4 的語法是 - GMT 5 的語法則是

.. GMT 5 is released in 2013 and is the latest major version of GMT [2]. It is also the version this tutorial is based. The major change of GMT 5 from GMT 4 is to “concentrate” all the commands into a single command gmt. Let’s take 2 basic commands pscoast and gmtset as examples: on GMT 4, the syntax is

.. $ gmt pscoast 各種選項... 
.. $ gmt set 各種選項...          # 以「gmt」開頭的指令，「gmt」不需重複兩次
.. $ gmt gmtset 各種選項...       # 但實際上如果你真的這麼輸入，也是 OK 的

.. 根據開發團隊的說法，此更動是為了避免 GMT 本身的指令與其他軟體的指令「撞名」。但為了相容舊版，某些 GMT 5 的版本會一併安裝指令的「捷徑」，這意味著不管你使用的是 GMT 4 的語法或是 GMT 5 的語法，程式都可以順利的讀取。在本教學手冊中，為了程式碼的簡潔，將\ **一律採用 GMT 4 的語法表示模式**\ ，而你則可以自由選擇自己喜歡的語法格式撰寫你的 GMT 腳本。

.. According to the development team, the change is to avoid the name conflict between GMT commands and commands from other software. However, to make GMT 5 compatible with old scripts, you can opt to install the “soft links” of all commands, which means GMT 5 can actually run any scripts, no matter the syntax they are based on. In this tutorial, we will use the style of GMT 4, i.e. without gmt in front of any commands, for greater code clarity. However, please feel free to choose the syntax you like to write your own GMT scripts.

PyGMT 的工作環境
--------------------------------------

.. _Python:

Python 與 PyGMT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Python 是\ `現在最流行的一種程式語言 <https://www.statista.com/chart/16567/popular-programming-languages/>`_。如果您對 Python 有興趣，網路上有非常多的學習資源。因為它非常流行，所以在 GMT 使用者社群中一直存在一股想法，就是希望能透過 Python 使用 GMT 的各項功能。GMT 是以 `C 語言 <https://zh.wikipedia.org/wiki/C%E8%AF%AD%E8%A8%80>`_\ 開發的，如果要使用 Python 存取 GMT 的函式庫，就要透過 API (應用程式介面，Application Programming Interface) 才能順利達成。GMT 的 API 本質上是額外的程式碼，但你可以把它想像成是不同線材的轉接頭，讓本質上是 C 語言的 GMT 函式庫能夠理解 Python 傳來的指令。PyGMT 就是透過 API 來下達繪圖指令給 GMT，並且再把 GMT 的回傳值 (地圖、數據等等) 整理成與 Python 相容的數據結構。這種軟體也稱為包裝庫 (Wrapper library)。


PyGMT 的語法簡介
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
PyGMT 把每張地圖視作一個\ `物件 <https://zh.wikipedia.org/wiki/%E5%AF%B9%E8%B1%A1_(%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6)>`_，然後透過物件的\ `方法 <https://zh.wikipedia.org/wiki/%E6%96%B9%E6%B3%95_(%E9%9B%BB%E8%85%A6%E7%A7%91%E5%AD%B8)>`_\ 來執行所有的繪圖指令。以 GMT 6 的 ``coast`` 指令來說，在 PyGMT 下你要這樣執行：

    .. code-block:: python

        import pygmt                # 首先必須匯入 PyGMT 模組！
        fig = pygmt.Figure()        # 建立地圖物件
        fig.coast(各種選項...)
        # 最後再用 fig.show() 螢幕出圖，或是 fig.savefig(...) 儲存圖檔


``coast`` 指令的各種選項，在 GMT 中是以 UNIX 風格的「旗標」模式指定，例如 ``-R``、``-J`` 等等。而在 PyGMT 中，不同的旗標被賦予了全名，並以參數值的格式輸入到物件方法中，例如 ``-R`` 對應到 ``region``，``-J`` 對應到 ``projection`` 等等。以下是來自「\ :doc:`making_first_map`\ 」的更詳細對照：


    .. code-block:: python

        # 使用 GMT 時... (在 shell 腳本中)
        gmt coast -R... -J... -W... -G... -B...
        # 使用 PyGMT 時... (在 python 腳本中)
        fig.coast(region=..., projection=..., shorelines=..., land=..., frame=...)

在 PyGMT 的使用手冊中，可以找到更詳細的\ `選項對照表格 <https://www.pygmt.org/latest/api/generated/pygmt.Figure.coast.html>`_。

Jupyter Notebook 與 Binder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
本教學手冊中使用兩種 PyGMT 腳本的格式。除了傳統的純文字 HTML 語法顯示外，也提供了 `Jupyter Notebook <https://jupyter.org/>`_ 的 Binder 連結。點開 Binder 連結後，伺服器端會安裝一個可以執行 PyGMT 的環境，然後你就可以透過你的網頁瀏覽器執行與修改教學手冊中的 PyGMT 程式碼。本功能目前使用 `MyBinder.org <https://mybinder.org/>`_ 提供、利用 Amazon Web Services 的雲端運算服務讓各位都能免安裝就體驗 PyGMT。歡迎各位多加嘗試！



.. [1] `Taiwan datums <https://wiki.osgeo.org/wiki/Taiwan_datums>`_, OSGeo Wiki.
.. [2] Wessel, P., Luis, J., Uieda, L., Scharroo, R., Wobbe, F., Smith, W. H. F., 
       and Tian, D. (2019). The Generic Mapping Tools Version 6. Geochemistry, 
       Geophysics, Geosystems, 20. 
       `doi.org/10.1029/2019GC008515 <http://doi.org/10.1029/2019GC008515>`_.

.. Wessel, P., W. H. F. Smith, R. Scharroo, J. Luis and F. Wobbe (2013), `Generic Mapping Tools: Improved Version Released <http://dx.doi.org/10.1002/2013EO450001>`_, Eos Trans. AGU, 94(45), 409.

.. 介紹 GIS Raster vs Vector
