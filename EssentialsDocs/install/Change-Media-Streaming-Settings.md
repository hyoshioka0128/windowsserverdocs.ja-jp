---
title: メディア ストリーミング設定の変更
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dec690d2-f80c-4b09-99d6-3bba41331972
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d34d60e792fcda4d71a4509fe3d1b95fc6e74d0e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823403"
---
# <a name="change-media-streaming-settings"></a>メディア ストリーミング設定の変更

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

メディア ストリーミング設定を変更するには、複数のオプションを使用できます。 次のオプションが使用できます。  
  
-   [リモート メディア ストリーミング アドインを非表示にします。](Change-Media-Streaming-Settings.md#BKMK_DisableRemote)  
  
-   [メディア ライブラリの名前を設定します。](Change-Media-Streaming-Settings.md#BKMK_LibraryName)  
  
-   [ビデオ ストリーミングの品質を設定します。](Change-Media-Streaming-Settings.md#BKMK_StreamingQuality)  
  
-   [プログラムによって有効またはメディア ストリーミングを無効にします。](Change-Media-Streaming-Settings.md#BKMK_Program)  
  
##  <a name="BKMK_DisableRemote"></a> リモート メディア ストリーミング アドインを非表示にします。  
 リモート メディア ストリーミング アドインを非表示にするには、レジストリのエントリを追加します。  
  
#### <a name="to-hide-the-remote-media-streaming-add-in"></a>リモート メディア ストリーミング アドインを非表示にするには  
  
1.  サーバーで、カーソルを画面の右上隅に移動して、**[検索]** をクリックします。  
  
2.  **[検索]** ボックスに「 **regedit**」と入力して、 **Regedit** アプリケーションをクリックします。  
  
3.  左側のウィンドウで、次のレジストリ エントリまで展開します。  
  
     **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\RemoteAccess\DisabledAddIns**  
  
4.  **[DisabledAddIns]** を右クリックし、**[新規]** をクリックし、**[DWORD 値]** をクリックします。  
  
5.  新しい値に「 **497796c6-9cc7-43be-aa26-4e6b5695370d**」 (リモート メディア ストリーミング アドインの識別子) と入力して、 **Enter**キーを押します。  
  
6.  値を右クリックして、**[変更]** をクリックします。  
  
7.  値データに「 **1** 」と入力し、**[OK]** をクリックします。  
  
##  <a name="BKMK_LibraryName"></a> メディア ライブラリの名前を設定します。  
 Windows Server Solutions SDK のクラスを使用して、メディア ライブラリ名を設定できます。 メディア ライブラリ名を設定するには、 **Microsoft.WindowsServerSolutions.MediaStreaming** 名前空間の **MediaStreamingManager** クラスの **SetMediaLibraryName** メソッドを使用します。 次の例では、メディア ライブラリ名を設定する方法を示します。  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
string mediaLibraryName = Guid.NewGuid().ToString("B");   
mediaStreamingManager.SetMediaLibraryName(mediaLibraryName);  
  
```  
  
 詳細については、 [Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)を参照してください。  
  
##  <a name="BKMK_StreamingQuality"></a> ビデオ ストリーミングの品質を設定します。  
 ビデオ ストリーミングの品質を設定するには、WinSAT CPU スコアを取得し、WinSAT スコア情報を含む .xml ファイルを作成およびインストールします。 初期構成を実行する前に WinSAT スコア情報を含む .xml ファイルをインストールすると、ビデオ品質の設定のためのユーザー インターフェイスがお客様の画面に表示されなくなります。 詳細については、「 [Set the WinSAT Score on the Server](Set-the-WinSAT-Score-on-the-Server.md)」を参照してください。  
  
##  <a name="BKMK_Program"></a> プログラムによって有効またはメディア ストリーミングを無効にします。  
 Windows Server Solutions SDK のクラスを使用して、プログラムによってメディア ストリーミングを有効または無効にできます。 メディア ストリーミングを有効または無効にするには、**Microsoft.WindowsServerSolutions.MediaStreaming** 名前空間の **MediaStreamingManager** クラスの **SetMediaStreamingEnabled** メソッドを使用します。 次のコード例は、メディア ストリーミングを有効にする方法を示します。  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(true);  
  
```  
  
 次のコード例は、メディア ストリーミングを無効にする方法を示します。  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(false);  
```  
  
## <a name="see-also"></a>関連項目  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)