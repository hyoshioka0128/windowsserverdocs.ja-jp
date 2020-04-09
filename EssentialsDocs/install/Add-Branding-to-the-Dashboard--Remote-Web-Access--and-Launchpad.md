---
title: ダッシュボード、リモート Web アクセス、スタート パッドへのブランドの追加
description: Windows Server Essentials の使用方法について説明します。
ms.date: 04/10/2014
ms.prod: windows-server
ms.topic: article
ms.assetid: 166262f8-b2a5-4b1c-a4a7-a141e1c54f10
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 50f132d7f6422c32b2a72948ca96b5bd82e701df
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817745"
---
# <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a>ダッシュボード、リモート Web アクセス、スタート パッドへのブランドの追加

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a><a name="BKMK_Branding"></a>ダッシュボード、リモート Web アクセス、スタートパッドにブランドを追加する  
 レジストリにエントリを追加することによって、多くのブランド追加を実行できます。 オペレーティング システムのレジストリ内のすべてのブランド エントリは、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OEM の下にあります。  
  
 すべてのブランド提携は、次のロゴの要件を満たしている必要があります。  
  
-   Windows Server Essentials ロゴは、正しい縦横比を維持したまま、 **96 DPI**で**170 ピクセル**の最小幅を持つ必要があります。  
  
#### <a name="to-add-branding-by-changing-the-registry"></a>レジストリを変更することでブランドを追加するには  
  
1.  サーバーで、カーソルを画面の右上隅に移動して、 **[検索]** をクリックします。  
  
2.  検索ボックスに「**regedit**」と入力して、 **[Regedit]** アプリケーションをクリックします。  
  
3.  ナビゲーション ウィンドウで、 **[HKEY_LOCAL_MACHINE]** 、 **[SOFTWARE]** 、 **[Microsoft]** 、 **[Windows Server]** の順に展開します。 **[OEM]** キーが存在しない場合は、キーを作成するために次の手順を実行します。  
  
    1.  **[Windows Server]** を右クリックし、 **[新規]** をクリックし、 **[キー]** をクリックします。  
  
    2.  キーの名前に「**OEM**」と入力します。  
  
4.  (省略可能) ロゴのエントリを作成している場合、ロゴの言語バージョンを区別するために異なるキーを作成できます。 たとえば、英語バージョンのロゴとドイツ語バージョンのロゴを所有する場合、en-us キーと de-de キーを作成できます。 ロゴ ファイルはすべて同じフォルダーに保存されるため、ロゴ イメージ ファイルのインスタンスに、言語ごとに一意の名前を指定する必要があります。 たとえば、DashboardLogo_en.png と DashboardLogo_de.png という名前のファイルを作成します。  
  
5.  **[OEM]** を右クリックするか、該当する言語キーを右クリックし、 **[新規]** をクリックし、 **[文字列値]** をクリックします。  
  

6.  文字列の名前を入力し、Enter キーを押します。 文字列名とデータ値については、表「[レジストリの文字列と値](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings)」を参照してください。  

6.  文字列の名前を入力し、Enter キーを押します。 文字列名とデータ値については、表「[レジストリの文字列と値](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings)」を参照してください。  

  
7.  新しい文字列を右クリックして、 **[変更]** をクリックします。  
  
8.  文字列名に関連する表から値を入力し、 **[OK]** をクリックします。  
  
9. ロゴ イメージまたは追加されたリンクのエントリを作成している場合、ファイルを %programFiles%\Windows Server\Bin\OEM にコピーします。 OEM ディレクトリが存在しない場合は、ディレクトリを作成します。  
  
10. リモート Web アクセスに影響を及ぼす変更が行われた場合、顧客はサーバーの所有権を得た後に、リモート Web アクセスを有効にする必要があります。 以下を実行することを顧客に通知します。  
  
    1.  ダッシュボードで、 **[設定]** をクリックし、 **[Anywhere Access]** タブをクリックします。  
  
    2.  Anywhere Access がオンになっている場合、**構成** をクリックし、次に Anywhere Access のセットアップ ウィザードの **有効にする Anywhere Access の機能を選択します** ページで、リモート Web アクセス チェック ボックスをオフにします。  
  
    3.  **[構成]** をクリックします。  
  
###  <a name="the-following-table-lists-the-location-where-registry-changes-affect-branding-the-string-name-and-the-data-value"></a><a name="BKMK_RegStrings"></a>次の表は、レジストリの変更がブランド、文字列名、およびデータ値に影響を与える場所を示しています。  
  
### <a name="registry-strings-and-values"></a>レジストリの文字列と値  
  
|ブランドの場所|説明|文字列名|データ値|  
|--------------------------|-----------------|-----------------|----------------|  
|ダッシュボードのロゴ|ロゴのイメージをダッシュボードに追加します。 ダッシュボードのロゴは .png 形式にし、幅 350 ピクセル、高さ 38 ピクセルを超えないようにする必要があります。<br /><br /> **重要:** ダッシュボードをロゴと共同でブランド化するには、OPK DVD に収録されているアートワークタイルを編集し、適切な空白の要件に従って、会社のロゴをイメージに追加する必要があります。 詳細については、提供されたタイル例を参照してください。|DashboardLogo|ロゴ イメージ ファイルの名前|  
|DashboardClientLogo|ダッシュボード クライアント ログイン画面に、ロゴのイメージを追加します。|DashboardClientLogo|ロゴ イメージ ファイルの名前|  
|Web サイトの背景画像|[リモート Web アクセス] ログオン ページに表示されている背景の画像を変更します。 一般的な解像度では、次のように表示されます。<br /><br /> -1024x768 ピクセル解像度を設定すると、ログオンページが正確に入力されます。<br /><br /> -800x600 ピクセル解像度はページの中央に配置され、黒い枠線で表示されます<br /><br /> -1280 x 720 ピクセル解像度が中央に配置され、1024x768 を超えるピクセルは表示されません|LogonBackground|背景のイメージ ファイルの名前|  
|Web サイトのタイトル|リモート Web アクセスサイトのタイトルを Windows Server Essentials から、選択したタイトルに置き換えます。|WebsiteName|新しいリモート Web アクセス サイトのタイトル|  
|Web サイトのロゴ|リモート Web アクセス サイトの既定のロゴを変更します。 予想されるロゴ サイズは 32 × 32 ピクセルです。 ロゴがこれより小さいか大きい場合、この寸法に合わせて拡大または縮小されます。|WebsiteLogo|ロゴ イメージ ファイルの名前|  
|追加された Web サイトのロゴ|パートナーのロゴは、リモート Web アクセス サイトに表示される Microsoft ロゴの真下に表示されます。 予想されるロゴ サイズは高さ 200 ピクセル、幅 50 ピクセルです。 ロゴがこれより大きい場合、元の縦横比を保持した状態でサイズに合わせて縮小されます。 ロゴがこれより小さい場合は、200 x 50 ピクセルのスペースの中央に配置され、サイズも縦横比も変更されません。|OEMLogo|ロゴ イメージ ファイルの名前|  

|Web サイトのホームページとログオンページのリンク |リモート Web アクセスサイトのログオンページとホームページへのリンクを追加します。 リンク情報が含まれる .xml は、%programFiles%\Windows Server\Bin\OEM に存在する必要があります。 次の例は、.xml ファイルの形式を示しています。<br /><br /> OemLinks の <\><br /> LogonLinks の <\><br /> < リンク名\=LogonLinkName ><br /> < テキスト\>LogonLinkDescription </Text\><br /> < Url\>LogonLinkURL </Url\><br /> < アイコン\>リンクアイコン </アイコン\><br /> </Link\><br /> </logonlinks\><br /> < HomepageLinks\><br /> < リンク名\=HomepageLinkName ><br /> < Text\>HomepageLinkDescription </Text\><br /> < Url\>HomepageLinkURL </Url\><br /> </Link\><br /> </HomepageLinks\><br /> </oemlinks\>|LinksXML |要素と説明の一覧については、 [LinksXML elements](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links)テーブルを参照してください |。  

|Web サイトのホームページとログオンページのリンク |リモート Web アクセスサイトのログオンページとホームページへのリンクを追加します。 リンク情報が含まれる .xml は、%programFiles%\Windows Server\Bin\OEM に存在する必要があります。 次の例は、.xml ファイルの形式を示しています。<br /><br /> OemLinks の <\><br /> LogonLinks の <\><br /> < リンク名\=LogonLinkName ><br /> < テキスト\>LogonLinkDescription </Text\><br /> < Url\>LogonLinkURL </Url\><br /> < アイコン\>リンクアイコン </アイコン\><br /> </Link\><br /> </logonlinks\><br /> < HomepageLinks\><br /> < リンク名\=HomepageLinkName ><br /> < Text\>HomepageLinkDescription </Text\><br /> < Url\>HomepageLinkURL </Url\><br /> </Link\><br /> </HomepageLinks\><br /> </oemlinks\>|LinksXML |要素と説明の一覧については、 [LinksXML elements](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links)テーブルを参照してください |。  

|スタートパッドのロゴ |ロゴイメージをスタートパッドに追加します。 スタートパッドのロゴは .png 形式である必要があり、64ピクセルを超える高さにすることはできません |。LaunchpadLogo |ロゴイメージファイルの名前 |  
  
###  <a name="the-following-table-lists-and-describes-the-linksxml-string-name-elements"></a><a name="BKMK_Links"></a>次の表に、LinksXML string name 要素の一覧とその説明を示します。  
  
### <a name="linksxml-elements"></a>LinksXML 要素  
  
|LinksXML 要素|説明|  
|----------------------|-----------------|  
|**LogonLinks**|  
|LogonLinkName|ログオンのリンク名です。|  
|LogonLinkDescription|ログオン ページのリンクとして表示されるテキストです。|  
|LogonLinkURL|ログオン ページのリンクを解決する URL です。|  
|LinkIcon|ログオンのリンクのアイコン ファイルの名前です。 このファイルは、.xml ファイルと同じフォルダー場所に存在する必要があります。 リンク アイコンのイメージは 16 x 16 ピクセルで、.png 形式にする必要があります。 LinkIcon を指定しない場合、既定のリンク アイコン イメージが使用されます。|  
|**HomepageLinks**|  
|HomepageLinkName|ホームページのリンク名です。|  
|HomepageLinkDescription|ホームページのリンクとして表示されるテキストです。|  
|HomepageLinkURL|ホームページのリンクを解決する URL です。|  
|HomepageLinkIcon|ホームページのリンクのアイコン ファイルの名前です。 このファイルは、.xml ファイルと同じフォルダー場所に存在する必要があります。 HomepageLinkIcon イメージは 16 x 16 ピクセルで、.png 形式にする必要があります。 HomepageLinkIcon を指定しない場合、既定のホーム ページ リンク アイコン イメージが使用されます。|  
  
## <a name="see-also"></a>参照  

 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [イメージ  の作成とカスタマイズ](../install/Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [展開  のイメージの準備](../install/Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

