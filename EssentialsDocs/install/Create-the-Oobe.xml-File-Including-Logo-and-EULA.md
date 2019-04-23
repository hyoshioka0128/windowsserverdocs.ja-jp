---
title: ロゴおよび EULA を含む Oobe.xml ファイルの作成
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a7b3cc1-21bb-4344-8110-f5d5959b370d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f8f99a2051e114b3c890f1cdac23aebf58689980
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884653"
---
# <a name="create-the-oobexml-file-including-logo-and-eula"></a>ロゴおよび EULA を含む Oobe.xml ファイルの作成

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Oobe.xml ファイルを使用して独自の使用許諾契約 (EULA) を初期構成に追加できます。 Oobe.xml は、初期構成、Windows へようこそ、およびエンド ユーザーに表示されるその他のページ用に、テキストとイメージを提供するために使用されるファイルです。 複数の Oobe.xml ファイルを追加して、エンド ユーザーの言語および国または地域選択に基づいて内容をカスタマイズできます。 詳細については、「 [Windows 8 用 Windows アセスメント &amp; デプロイメント キット](https://go.microsoft.com/fwlink/?LinkId=248694) 」を参照してください。  
  
 会社の EULA は、Microsoft EULA に加えて表示されます。 Microsoft EULA が初期構成エンド ユーザー エクスペリエンス中に表示される最初の EULA で、次にユーザーの EULA が表示されます。 ユーザーの EULA はサーバーの任意の場所に配置でき、場所は Oobe.xml ファイルに指定します。  
  
#### <a name="to-add-your-company-eula-and-logo"></a>会社の EULA とロゴを追加するには  
  
1.  Oobe.xml ファイルをメモ帳などのテキスト エディターで開きます。  
  
2.  内で、< logopath\></logopath\>タグに、ロゴ ファイルへの絶対パスを入力します。 このファイルには、240 x 100 ピクセルの 32 ビット ポータブル ネットワーク グラフィックス (.png) ファイルが含まれます。  
  
3.  内で、< eulafilename\></eulafilename\>タグ、EULA ファイルへの絶対パスを入力します。 EULA ファイルはリッチ テキスト形式 (.rtf) ファイルでなければなりません。  
  
4.  内で、< 名前\></name\>タグ、会社名を入力します。  
  
     次の例は、Oobe.xml ファイル内のタグを示しています。  
  
    ```  
  
    <FirstExperience>  
       <oobe>  
          <oem>  
             <name>Fabrikam</name>  
             <logopath>c:\fabrikam\fabrikam.png</logopath>  
             <eulafilename>c:\fabrikam\fabrikam_eula.rtf</eulafilename>  
          </oem>  
       </oobe>  
    </FirstExperience>  
  
    ```  
  
5.  ファイルを保存します。  
  
6.  Oobe.xml ファイルを次のいずれかの場所に配置します。  
  
    |Oobe.xml の場所|場所を決定する条件|  
    |-----------------------|----------------------------------------|  
    |%windir%\system32\oobe\info\|サーバーは 1 つの国/地域および単一言語システムで出荷されます。|  
    |%windir%\system32\oobe\info\default\\< 言語\>|サーバーは、単一の国/地域および多言語システムで出荷されています。|  
    |%windir%\system32\oobe\info\\< 国/地域 > \ と %windir%\system32\oobe\info\\< 国/地域 >\\< 言語\>\|サーバーは 1 つ以上の国に出荷/リージョンと、設定には、それぞれに 1 つの言語、国/地域ごとにカスタマイズが必要です。 国または、サーバーがデプロイされているリージョンの地理的な場所識別子 (GeoID) の 10 進数バージョンが < 国/地域 > と < 言語\>はロケール識別子 (LCID) の 10 進数のバージョンです。|  
  
 文字が白の会社ロゴがある場合、セットアップ フローは背景色が青であるため、セットアップ フローで表示すると効果的です。  このロゴを任意で指定するには、レジストリ キーと値を設定します。  
  
#### <a name="to-specify-a-company-logo-by-setting-the-oem-registry-key"></a>会社ロゴを指定するため OEM レジストリ キーを設定するには  
  
1.  サーバーで、カーソルを画面の右上隅に移動して、**[検索]** をクリックします。  
  
2.  検索ボックスに「 **regedit**」と入力して、Regedit アプリケーションをクリックします。  
  
3.  ナビゲーション ウィンドウで、**[HKEY_LOCAL_MACHINE]** に移動し、**[SOFTWARE]**、**[Microsoft]**、**[Windows Server]** の順に展開します。 OEM キーが存在しない場合、次の手順でキーを作成します。  
  
    1.  **[Windows Server]** を右クリックし、**[新規]** をクリックし、**[キー]** をクリックします。  
  
    2.  キー名に「**OEM**」と入力します。  
  
4.  (省略可能) ロゴのエントリを作成している場合、ロゴの言語バージョンを区別するために異なるキーを作成できます。 たとえば、英語バージョンのロゴとドイツ語バージョンのロゴを所有する場合、en-us キーと de-de キーを作成できます。 ロゴ ファイルはすべて同じフォルダーに保存されるため、ロゴ イメージ ファイルのインスタンスに、言語ごとに一意の名前を指定する必要があります。 たとえば、LogoWithWhiteText_en.png と LogoWithWhiteText_de.png という名前のファイルを作成します。  
  
5.  **[OEM]** を右クリックするか、該当する言語キーを右クリックし、**[新規]** をクリックし、**[文字列値]** をクリックします。  
  
6.  文字列として「LogoWithWhiteText」を入力し、Enter キーを押します。  
  
7.  新しい文字列を右クリックして、**[変更]** をクリックします。  
  
8.  ロゴ イメージを含むパスを入力し、[OK] をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)