---
title: "ロゴおよび EULA を含む Oobe.xml ファイルを作成します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-the-oobexml-file-including-logo-and-eula"></a>ロゴおよび EULA を含む Oobe.xml ファイルを作成します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Oobe.xml ファイルを使用して、初期構成を独自のエンド ユーザー ライセンス契約 (EULA) を追加できます。 Oobe.xml は、初期構成、Windows へようこそ、およびその他のページのエンド ユーザーに表示されるテキストと画像を提供するためのファイルです。 エンド ユーザーの言語および国または地域選択に基づいてコンテンツをカスタマイズする複数の Oobe.xml ファイルを追加することができます。 詳細については、次を参照してください。、[Windows アセスメント & デプロイメント キット for Windows 8](https://go.microsoft.com/fwlink/?LinkId=248694)ドキュメントです。  
  
 会社の EULA は、Microsoft EULA に加えて表示されます。 最初の EULA が初期構成エンド ユーザー エクスペリエンス、中に表示される Microsoft EULA がし、使用許諾契約書が表示されます。 サーバーで、使用許諾契約書をどこにでも配置でき、Oobe.xml ファイルの場所を指定します。  
  
#### <a name="to-add-your-company-eula-and-logo"></a>会社の EULA とロゴを追加するには  
  
1.  Oobe.xml ファイルをメモ帳などのテキスト エディターで開きます。  
  
2.  < Logopath\ >< 内/logopath\ > タグに、ロゴ ファイルへの絶対パスを入力してください。 このファイルは、240 x 100 ピクセルである 32 ビット ポータブル ネットワーク グラフィックス (.png) ファイルが含まれている必要があります。  
  
3.  < Eulafilename\ >< 内/eulafilename\ > タグ、EULA ファイルの絶対パスを入力します。 EULA ファイルはリッチ テキスト形式 (.rtf) ファイルである必要があります。  
  
4.  < 名前 \/>< 内/名前 \/> タグは、会社名を入力します。  
  
     次の例では、Oobe.xml ファイルにタグを示しています。  
  
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
  
6.  次の場所のいずれかで、Oobe.xml ファイルを配置します。  
  
    |Oobe.xml の場所|場所を決定する条件|  
    |-----------------------|----------------------------------------|  
    |%windir%\system32\oobe\info\|サーバーは単一の国/地域および単一言語システムで出荷されています。|  
    |%windir%\system32\oobe\info\default\\ < 言語 >|サーバーは単一の国/地域および多言語システムで出荷されています。|  
    |%windir%\system32\oobe\info\\ < 国/地域 > \ < 国/地域 > %windir%\system32\oobe\info\\ と \\ < 言語 > \|サーバーは 1 つ以上の国/地域に出荷し、設定は、それぞれ単一言語と国/地域ごとにカスタマイズを必要とします。 ここで < 国/地域 > は、国または地域で、サーバーが展開されている、< 言語 > はロケール識別子 (LCID) の 10 進数バージョンの地理的な場所識別子 (GeoID) の 10 進数バージョンです。|  
  
 ある場合は白色のテキストで、別の会社のロゴ、フレンドと背景色が青のため、セットアップ フローが表示されます。  レジストリ キーと値を設定して、必要に応じてこのロゴを指定することができます。  
  
#### <a name="to-specify-a-company-logo-by-setting-the-oem-registry-key"></a>OEM レジストリ キー設定によって、会社のロゴを指定するには  
  
1.  サーバーで、マウスを移動して、画面の右上隅とクリックして**検索**します。  
  
2.  検索ボックスに次のように入力します。**regedit**、Regedit アプリケーションをクリックします。  
  
3.  移動し、ナビゲーション ウィンドウで、**HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、展開**Microsoft**、展開**Windows Server**します。 OEM キーが存在しない場合は、次のように、キーを作成します。  
  
    1.  右クリック**Windows Server**、] をクリックして**新規**、] をクリックし、**キー**します。  
  
    2.  キー名は、次のように入力します。**OEM**します。  
  
4.  (省略可能)ロゴのエントリを作成する場合は、ロゴの言語バージョンを区別するために異なるキーを作成できます。 たとえば、英語とドイツ語の両方のバージョンのロゴがあればを作成、en-キーと de-de キー。 すべてのロゴ ファイルが格納されるため、同じフォルダーに、言語ごとに一意の名前でロゴ イメージ ファイルのインスタンスを提供する必要があります。 たとえば、LogoWithWhiteText_en.png と LogoWithWhiteText_de.png という名前のファイルを作成することができます。  
  
5.  いずれかを右クリック**OEM**または該当する言語キーを右クリックし、クリックすると**新規**、] をクリックし、**文字列値**します。  
  
6.  を文字列として「logowithwhitetext」と入力し、、Enter キーを押します。  
  
7.  新しい文字列を右クリックし、をクリックして**変更**します。  
  
8.  ロゴのイメージを含むパスを入力し、[OK] をクリックします。  
  
## <a name="see-also"></a>参照してください。  
 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)