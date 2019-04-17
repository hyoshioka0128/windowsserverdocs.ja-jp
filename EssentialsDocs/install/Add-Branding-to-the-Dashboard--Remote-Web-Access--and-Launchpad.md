---
title: "ダッシュ ボード、リモート Web アクセス、スタート パッドへのブランドを追加します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a>ダッシュ ボード、リモート Web アクセス、スタート パッドへのブランドを追加します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

##  <a name="BKMK_Branding"></a>ダッシュ ボード、リモート Web アクセス、スタート パッドへのブランドを追加します。  
 レジストリにエントリを追加することで、多くのブランド追加を行うことができます。 オペレーティング システム用にレジストリ内のすべてのブランド エントリは、HKEY_LOCAL_MACHINE \software\microsoft\windows \OEM の下にあります。  
  
 すべてのブランド、次のロゴの要件を満たしている必要があります。  
  
-   Windows Server Essentials ロゴの最小の幅が必要**170 ピクセル**で、正しい縦横比を維持する**96 DPI**します。  
  
#### <a name="to-add-branding-by-changing-the-registry"></a>レジストリを変更することでブランドを追加するには  
  
1.  サーバーで、マウスを移動して、画面の右上隅とクリックして**検索**します。  
  
2.  検索ボックスに次のように入力します。**regedit**、クリックして、**Regedit**アプリケーション。  
  
3.  ナビゲーション ウィンドウで [ **HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、展開**Microsoft**、展開**Windows Server**します。 場合、**OEM**キーが存在して、作成時に、次の手順を完了していません。  
  
    1.  右クリック**Windows Server**、] をクリックして**新規**、] をクリックし、**キー**します。  
  
    2.  種類**OEM**、キーの名前。  
  
4.  (省略可能)ロゴのエントリを作成する場合は、ロゴの言語バージョンを区別するために異なるキーを作成できます。 たとえば、英語とドイツ語の両方のバージョンのロゴがあればを作成、en-キーと de-de キー。 すべてのロゴ ファイルが格納されるため、同じフォルダーに、言語ごとに一意の名前でロゴ イメージ ファイルのインスタンスを提供する必要があります。 たとえば、DashboardLogo_en.png と DashboardLogo_de.png という名前のファイルを作成します。  
  
5.  いずれかを右クリック**OEM**または該当する言語キーを右クリックし、クリックすると**新規**、] をクリックし、**文字列値**します。  
  

6.  文字列の名前を入力し、Enter キーを押します。 参照してください、[レジストリの文字列と値](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings)文字列名とデータ値のテーブルです。  

6.  文字列の名前を入力し、Enter キーを押します。 参照してください、[レジストリの文字列と値](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings)文字列名とデータ値のテーブルです。  

  
7.  新しい文字列を右クリックし、をクリックして**変更**します。  
  
8.  文字列名に関連付けられているテーブルから値を入力し、クリックして**OK**します。  
  
9. ロゴ イメージまたは追加されたリンクのエントリを作成する場合は、ファイルを %programFiles%\Windows server \bin\OEM にコピーします。 OEM ディレクトリが存在しない場合は、それを作成します。  
  
10. 変更を行った後、お客様が所有しているサーバーのリモート Web アクセスに影響する場合は、リモート Web アクセスに必要があります。 お手数ですが、顧客が、次の操作をします。  
  
    1.  ダッシュ ボードで、をクリックして**設定**、クリックして、**Anywhere Access** ] タブ。  
  
    2.  Anywhere Access がオンの場合] をクリックして**構成**でリモート Web アクセスのチェック ボックスをクリアし、**Anywhere Access 機能の選択を有効にする**の Anywhere Access のウィザードのセットアップ] ページ。  
  
    3.  をクリックして**構成**します。  
  
###  <a name="BKMK_RegStrings"></a>次の表は、レジストリ変更影響を与えてブランドの場所、文字列名、およびデータ値を示します。  
  
### <a name="registry-strings-and-values"></a>レジストリの文字列と値  
  
|ブランドの場所|説明|文字列名|データ値|  
|--------------------------|-----------------|-----------------|----------------|  
|ダッシュ ボードのロゴ|ダッシュ ボードに、ロゴのイメージを追加します。 ダッシュ ボードのロゴは .png 形式にする必要があります、幅 350 ピクセル、高さ 38 ピクセルを超えていない必要があります。<br /><br /> **重要:**ロゴでダッシュ ボードをブランド提携する、OPK DVD で提供され、適切な余白の要件の実行中に、会社のロゴをイメージに追加いるアートワーク タイルを編集する必要があります。 追加情報提供されたタイル例をご覧ください。|DashboardLogo|ロゴ イメージ ファイルの名前|  
|DashboardClientLogo|ダッシュ ボード クライアント ログイン画面に、ロゴのイメージを追加します。|DashboardClientLogo|ロゴ イメージ ファイルの名前|  
|Web サイトの背景画像|リモート Web アクセスのログオン ページに表示される背景画像を変更します。 典型的な解像度は、次のように表示されます。<br /><br /> -1024 x 768 ピクセルの解像度は正確な場合、ログオン ページ<br /><br /> -800 x 600 ピクセルの解像度] ページで中央に配置して、黒の境界線が表示されます。<br /><br /> -1280 x 720 ピクセルの解像度を中央に配置して、1024 x 768 を超えるピクセルは表示されません。|LogonBackground|バック グラウンド イメージ ファイルの名前|  
|Web サイトのタイトル|Windows Server Essentials から選択したタイトルにリモート Web アクセス サイトのタイトルに置き換えます。|WebsiteName|新しいリモート Web アクセス サイトのタイトル|  
|Web サイトのロゴ|リモート Web アクセス サイトの既定のロゴを変更します。 予想されるロゴ サイズは、32 ピクセルの 32 ピクセルです。 ロゴがこれより大きいまたは小さい場合が拡大または、これらの寸法に合わせて縮小|WebsiteLogo|ロゴ イメージ ファイルの名前|  
|追加された Web サイトのロゴ|リモート Web アクセス サイトに表示される Microsoft ロゴの真下パートナーのロゴが表示されます。 予想されるロゴ サイズは、高さ 200 ピクセル、幅 50 ピクセルです。 ロゴがこれより大きい場合は、その行われます小さい元の縦横比を維持しながら、それに合わせて。 かどうかロゴがこれより小さい場合、200 x 50 ピクセルのスペースの中央に配置されますが、サイズも縦横比が変更されます。|OEMLogo|ロゴ イメージ ファイルの名前|  

|Web サイトのホーム ページとログオン ページのリンク |ログオン ページとリモート Web アクセス サイトのホーム ページにリンクを追加します。 リンク情報が含まれる .xml は、%programFiles%\Windows server \bin\OEM に存在する必要があります。 次の例は、.xml ファイルの形式を示しています。<br /><br /> < OemLinks\ ><br /> < LogonLinks\ ><br /> < リンクの名前 \/LogonLinkName を = ><br /> < テキスト > LogonLinkDescription </テキスト ><br /> < Url\ > LogonLinkURL </Url\ ><br /> < Icon\ > LinkIcon </Icon\ ><br /> </Link\ ><br /> </LogonLinks\ ><br /> < HomepageLinks\ ><br /> < リンクの名前 \/HomepageLinkName を = ><br /> < テキスト > HomepageLinkDescription </テキスト ><br /> < Url\ > HomepageLinkURL </Url\ ><br /> </Link\ ><br /> </HomepageLinks\ ><br /> </OemLinks\ > |LinksXML |参照してください、[LinksXML 要素](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links)要素とその説明の一覧については表 |。  

|Web サイトのホーム ページとログオン ページのリンク |ログオン ページとリモート Web アクセス サイトのホーム ページにリンクを追加します。 リンク情報が含まれる .xml は、%programFiles%\Windows server \bin\OEM に存在する必要があります。 次の例は、.xml ファイルの形式を示しています。<br /><br /> < OemLinks\ ><br /> < LogonLinks\ ><br /> < リンクの名前 \/LogonLinkName を = ><br /> < テキスト > LogonLinkDescription </テキスト ><br /> < Url\ > LogonLinkURL </Url\ ><br /> < Icon\ > LinkIcon </Icon\ ><br /> </Link\ ><br /> </LogonLinks\ ><br /> < HomepageLinks\ ><br /> < リンクの名前 \/HomepageLinkName を = ><br /> < テキスト > HomepageLinkDescription </テキスト ><br /> < Url\ > HomepageLinkURL </Url\ ><br /> </Link\ ><br /> </HomepageLinks\ ><br /> </OemLinks\ > |LinksXML |参照してください、[LinksXML 要素](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links)要素とその説明の一覧については表 |。  

|スタート パッドのロゴ |ロゴのイメージをスタート パッドに追加します。 スタート パッドのロゴは .png 形式である必要がない高さ 64 ピクセルより高いにする必要があります |。LaunchpadLogo |ロゴ イメージ ファイルの名前 |  
  
###  <a name="BKMK_Links"></a>次の表は、LinksXML の文字列名の要素の一覧です。  
  
### <a name="linksxml-elements"></a>LinksXML 要素  
  
|LinksXML 要素|説明|  
|----------------------|-----------------|  
|**LogonLinks**|  
|LogonLinkName|ログオンのリンク名です。|  
|LogonLinkDescription|ログオン ページのリンクとして表示されるテキストです。|  
|LogonLinkURL|ログオン ページのリンクを解決する url です。|  
|LinkIcon|ログオンのリンクのアイコン ファイルの名前。 このファイルは、.xml ファイルと同じフォルダー場所にする必要があります。 リンク アイコン イメージは 16 x 16 ピクセルをする必要があります、.png 形式にする必要があります。 LinkIcon を指定しない場合は、既定のリンク アイコン イメージが使用されます。|  
|**HomepageLinks**|  
|HomepageLinkName|ホームページのリンク名です。|  
|HomepageLinkDescription|ホームページのリンクとして表示されるテキストです。|  
|HomepageLinkURL|ホームページのリンクを解決する URL です。|  
|HomepageLinkIcon|ホームページのリンクのアイコン ファイルの名前。 このファイルは、.xml ファイルと同じフォルダー場所にする必要があります。 HomepageLinkIcon イメージは 16 x 16 ピクセルをする必要があります、.png 形式にする必要があります。 HomepageLinkIcon を指定しない場合、既定のホーム ページ リンク アイコン イメージが使用されます。|  
  
## <a name="see-also"></a>参照してください。  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

