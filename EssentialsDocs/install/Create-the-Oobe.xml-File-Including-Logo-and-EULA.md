---
title: ロゴおよび EULA を含む Oobe.xml ファイルの作成
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a7b3cc1-21bb-4344-8110-f5d5959b370d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 58d98aa84b8851e3226ebc76c86cffd574400c42
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312057"
---
# <a name="create-the-oobexml-file-including-logo-and-eula"></a>ロゴおよび EULA を含む Oobe.xml ファイルの作成

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Oobe.xml ファイルを使用して独自の使用許諾契約 (EULA) を初期構成に追加できます。 Oobe.xml は、初期構成、Windows へようこそ、およびエンド ユーザーに表示されるその他のページ用に、テキストとイメージを提供するために使用されるファイルです。 複数の Oobe.xml ファイルを追加して、エンド ユーザーの言語および国または地域選択に基づいて内容をカスタマイズできます。 詳細については、「 [Windows 8 用 Windows アセスメント &amp; デプロイメント キット](https://go.microsoft.com/fwlink/?LinkId=248694) 」を参照してください。  
  
 会社の EULA は、Microsoft EULA に加えて表示されます。 Microsoft EULA が初期構成エンド ユーザー エクスペリエンス中に表示される最初の EULA で、次にユーザーの EULA が表示されます。 ユーザーの EULA はサーバーの任意の場所に配置でき、場所は Oobe.xml ファイルに指定します。  
  
#### <a name="to-add-your-company-eula-and-logo"></a>会社の EULA とロゴを追加するには  
  
1. Oobe.xml ファイルをメモ帳などのテキスト エディターで開きます。  
  
2. < Logopath\></logopath\> タグ内に、ロゴファイルへの絶対パスを入力します。 このファイルには、240 x 100 ピクセルの 32 ビット ポータブル ネットワーク グラフィックス (.png) ファイルが含まれます。  
  
3. < Eulafilename\></eulafilename\> タグ内に、EULA ファイルへの絶対パスを入力します。 EULA ファイルはリッチ テキスト形式 (.rtf) ファイルでなければなりません。  
  
4. < 名\></name\> タグで、会社名を入力します。  
  
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
  
5. ファイルを保存します。  
  
6. Oobe.xml ファイルを次のいずれかの場所に配置します。  
  
   |Oobe.xml の場所|場所を決定する条件|  
   |-----------------------|----------------------------------------|  
   |%windir%\system32\oobe\info\|サーバーは、1つの国/地域と1つの言語システムで出荷されています。|  
   |%windir%\system32\oobe\info\default\\< 言語\>|サーバーは、単一の国/地域および多言語システムで出荷されています。|  
   |%windir%\system32\oobe\info\\< 国/地域 > \ と%windir%\system32\oobe\info\\< 国/地域 >\\< 言語\>\|サーバーは複数の国/地域に出荷されており、設定は国/地域ごとに1つの言語でカスタマイズする必要があります。 ここで < 国/地域 > は、サーバーが展開されている国または地域の地理的な場所識別子 (GeoID) の10進数バージョンであり、< 言語\> はロケール識別子 (LCID) の10進数バージョンです。|  
  
   文字が白の会社ロゴがある場合、セットアップ フローは背景色が青であるため、セットアップ フローで表示すると効果的です。  このロゴを任意で指定するには、レジストリ キーと値を設定します。  
  
#### <a name="to-specify-a-company-logo-by-setting-the-oem-registry-key"></a>会社ロゴを指定するため OEM レジストリ キーを設定するには  
  
1.  サーバーで、カーソルを画面の右上隅に移動して、 **[検索]** をクリックします。  
  
2.  検索ボックスに「**regedit**」と入力して、Regedit アプリケーションをクリックします。  
  
3.  ナビゲーション ウィンドウで、 **[HKEY_LOCAL_MACHINE]** に移動し、 **[SOFTWARE]** 、 **[Microsoft]** 、 **[Windows Server]** の順に展開します。 OEM キーが存在しない場合、次の手順でキーを作成します。  
  
    1.  **[Windows Server]** を右クリックし、 **[新規]** をクリックし、 **[キー]** をクリックします。  
  
    2.  キー名に「**OEM**」と入力します。  
  
4.  (省略可能) ロゴのエントリを作成している場合、ロゴの言語バージョンを区別するために異なるキーを作成できます。 たとえば、英語バージョンのロゴとドイツ語バージョンのロゴを所有する場合、en-us キーと de-de キーを作成できます。 ロゴ ファイルはすべて同じフォルダーに保存されるため、ロゴ イメージ ファイルのインスタンスに、言語ごとに一意の名前を指定する必要があります。 たとえば、LogoWithWhiteText_en.png と LogoWithWhiteText_de.png という名前のファイルを作成します。  
  
5.  **[OEM]** を右クリックするか、該当する言語キーを右クリックし、 **[新規]** をクリックし、 **[文字列値]** をクリックします。  
  
6.  文字列として「LogoWithWhiteText」を入力し、Enter キーを押します。  
  
7.  新しい文字列を右クリックして、 **[変更]** をクリックします。  
  
8.  ロゴ イメージを含むパスを入力し、[OK] をクリックします。  
  
## <a name="see-also"></a>参照  
 [Windows Server ESSENTIALS ADK でのはじめに](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)