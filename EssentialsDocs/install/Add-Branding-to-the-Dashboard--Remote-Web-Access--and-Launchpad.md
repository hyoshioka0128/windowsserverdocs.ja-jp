---
title: ダッシュボード、リモート Web アクセス、スタート パッドへのブランドの追加
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 04/10/2014
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 166262f8-b2a5-4b1c-a4a7-a141e1c54f10
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 02088b169e44cdcf87385425e1949232ffa408a6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823503"
---
# <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a>ダッシュボード、リモート Web アクセス、スタート パッドへのブランドの追加

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_Branding"></a> ダッシュ ボード、リモート Web アクセス、スタート パッドへのブランドを追加します。  
 レジストリにエントリを追加することによって、多くのブランド追加を実行できます。 オペレーティング システムのレジストリ内のすべてのブランド エントリは、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OEM の下にあります。  
  
 すべてのブランド提携は、次のロゴの要件を満たしている必要があります。  
  
-   Windows Server Essentials のロゴの最小幅をいる必要があります**170 ピクセル**で、正しい縦横比を維持する**96 DPI**します。  
  
#### <a name="to-add-branding-by-changing-the-registry"></a>レジストリを変更することでブランドを追加するには  
  
1.  サーバーで、カーソルを画面の右上隅に移動して、**[検索]** をクリックします。  
  
2.  検索ボックスに「**regedit**」と入力して、**[Regedit]** アプリケーションをクリックします。  
  
3.  ナビゲーション ウィンドウで、**[HKEY_LOCAL_MACHINE]**、**[SOFTWARE]**、**[Microsoft]**、**[Windows Server]** の順に展開します。 **[OEM]** キーが存在しない場合は、キーを作成するために次の手順を実行します。  
  
    1.  **[Windows Server]** を右クリックし、**[新規]** をクリックし、**[キー]** をクリックします。  
  
    2.  キーの名前に「**OEM**」と入力します。  
  
4.  (省略可能) ロゴのエントリを作成している場合、ロゴの言語バージョンを区別するために異なるキーを作成できます。 たとえば、英語バージョンのロゴとドイツ語バージョンのロゴを所有する場合、en-us キーと de-de キーを作成できます。 ロゴ ファイルはすべて同じフォルダーに保存されるため、ロゴ イメージ ファイルのインスタンスに、言語ごとに一意の名前を指定する必要があります。 たとえば、DashboardLogo_en.png と DashboardLogo_de.png という名前のファイルを作成します。  
  
5.  **[OEM]** を右クリックするか、該当する言語キーを右クリックし、**[新規]** をクリックし、**[文字列値]** をクリックします。  
  

6.  文字列の名前を入力し、Enter キーを押します。 文字列名とデータ値については、表「[レジストリの文字列と値](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings)」を参照してください。  

6.  文字列の名前を入力し、Enter キーを押します。 文字列名とデータ値については、表「[レジストリの文字列と値](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings)」を参照してください。  

  
7.  新しい文字列を右クリックして、**[変更]** をクリックします。  
  
8.  文字列名に関連する表から値を入力し、**[OK]** をクリックします。  
  
9. ロゴ イメージまたは追加されたリンクのエントリを作成している場合、ファイルを %programFiles%\Windows Server\Bin\OEM にコピーします。 OEM ディレクトリが存在しない場合は、ディレクトリを作成します。  
  
10. リモート Web アクセスに影響を及ぼす変更が行われた場合、顧客はサーバーの所有権を得た後に、リモート Web アクセスを有効にする必要があります。 以下を実行することを顧客に通知します。  
  
    1.  ダッシュボードで、**[設定]** をクリックし、**[Anywhere Access]** タブをクリックします。  
  
    2.  Anywhere Access がオンになっている場合、**[構成]** をクリックし、次に Anywhere Access のセットアップ ウィザードの **[有効にする Anywhere Access の機能を選択します]** ページで、[リモート Web アクセス チェック ボックスをオフにします。  
  
    3.  をクリックして**構成**です。  
  
###  <a name="BKMK_RegStrings"></a> 次の表は、レジストリの変更がブランド化に影響する、場所、文字列名、およびデータ値を示します。  
  
### <a name="registry-strings-and-values"></a>レジストリの文字列と値  
  
|ブランドの場所|説明|文字列名|データ値|  
|--------------------------|-----------------|-----------------|----------------|  
|ダッシュボードのロゴ|ロゴのイメージをダッシュボードに追加します。 ダッシュボードのロゴは .png 形式にし、幅 350 ピクセル、高さ 38 ピクセルを超えないようにする必要があります。<br /><br /> 概要ロゴを使用してダッシュボードをブランド提携するには、適切な余白の要件に従って、OPK DVD で提供されているアートワーク タイルを編集し、イメージに会社のロゴを追加する必要があります。 詳細については、提供されたタイル例を参照してください。|DashboardLogo|ロゴ イメージ ファイルの名前|  
|DashboardClientLogo|ダッシュボード クライアント ログイン画面に、ロゴのイメージを追加します。|DashboardClientLogo|ロゴ イメージ ファイルの名前|  
|Web サイトの背景画像|[リモート Web アクセス] ログオン ページに表示されている背景の画像を変更します。 一般的な解像度では、次のように表示されます。<br /><br /> -1024 x 768 ピクセルの解像度には、ログオン ページが納まります。<br /><br /> ~ 800 x 600 ピクセルの解像度 ページに表示して、黒い境界線が表示されます。<br /><br /> -1280 x 720 ピクセルの解像度が中央揃えにして、1024 x 768 を超えるピクセルは表示されません。|LogonBackground|背景のイメージ ファイルの名前|  
|Web サイトのタイトル|選択したタイトルを Windows Server Essentials からリモート Web アクセス サイトのタイトルに置き換えます。|WebsiteName|新しいリモート Web アクセス サイトのタイトル|  
|Web サイトのロゴ|リモート Web アクセス サイトの既定のロゴを変更します。 予想されるロゴ サイズは 32 × 32 ピクセルです。 ロゴがこれより小さいか大きい場合、この寸法に合わせて拡大または縮小されます。|WebsiteLogo|ロゴ イメージ ファイルの名前|  
|追加された Web サイトのロゴ|パートナーのロゴは、リモート Web アクセス サイトに表示される Microsoft ロゴの真下に表示されます。 予想されるロゴ サイズは高さ 200 ピクセル、幅 50 ピクセルです。 ロゴがこれより大きい場合、元の縦横比を保持した状態でサイズに合わせて縮小されます。 ロゴがこれより小さい場合は、200 x 50 ピクセルのスペースの中央に配置され、サイズも縦横比も変更されません。|OEMLogo|ロゴ イメージ ファイルの名前|  

|Web サイトのホーム ページとログオン ページのリンク |ログオン ページと、リモート Web アクセス サイトのホーム ページのリンクを追加します。 リンク情報が含まれる .xml は、%programFiles%\Windows Server\Bin\OEM に存在する必要があります。 次の例は、.xml ファイルの形式を示しています。<br /><br /> < OemLinks\><br /> <LogonLinks\><br /> <Link Name\=LogonLinkName><br /> <Text\>LogonLinkDescription</Text\><br /> < Url\>LogonLinkURL </の Url\><br /> < アイコン\>LinkIcon </ アイコン\><br /> </link\><br /> </LogonLinks\><br /> <HomepageLinks\><br /> <Link Name\=HomepageLinkName><br /> <Text\>HomepageLinkDescription</Text\><br /> < Url\>HomepageLinkURL </の Url\><br /> </link\><br /> </HomepageLinks\><br /> </OemLinks\>|LinksXML |参照してください、 [LinksXML 要素](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links)要素とその説明の一覧についてはテーブルです |。  

|Web サイトのホーム ページとログオン ページのリンク |ログオン ページと、リモート Web アクセス サイトのホーム ページのリンクを追加します。 リンク情報が含まれる .xml は、%programFiles%\Windows Server\Bin\OEM に存在する必要があります。 次の例は、.xml ファイルの形式を示しています。<br /><br /> < OemLinks\><br /> <LogonLinks\><br /> <Link Name\=LogonLinkName><br /> <Text\>LogonLinkDescription</Text\><br /> < Url\>LogonLinkURL </の Url\><br /> < アイコン\>LinkIcon </ アイコン\><br /> </link\><br /> </LogonLinks\><br /> <HomepageLinks\><br /> <Link Name\=HomepageLinkName><br /> <Text\>HomepageLinkDescription</Text\><br /> < Url\>HomepageLinkURL </の Url\><br /> </link\><br /> </HomepageLinks\><br /> </OemLinks\>|LinksXML |参照してください、 [LinksXML 要素](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links)要素とその説明の一覧についてはテーブルです |。  

|スタート パッドのロゴ |スタート パッドにロゴ イメージを追加します。 スタート パッドのロゴは .png 形式とする必要がありますいない高さ 64 ピクセルより高いである必要があります |。LaunchpadLogo |ロゴのイメージ ファイルの名前 |  
  
###  <a name="BKMK_Links"></a> 次の表を示し、LinksXML の文字列名要素について説明します。  
  
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
  
## <a name="see-also"></a>関連項目  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

