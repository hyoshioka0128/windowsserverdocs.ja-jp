---
title: メディア ストリーミング設定の変更
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dec690d2-f80c-4b09-99d6-3bba41331972
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 217bcbeda8f50ee1f17bcc1da6bd5b982dcf5106
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310073"
---
# <a name="change-media-streaming-settings"></a>メディア ストリーミング設定の変更

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

メディア ストリーミング設定を変更するには、複数のオプションを使用できます。 次のオプションが使用できます。  
  
-   [リモートメディアストリーミングアドインを非表示にする](Change-Media-Streaming-Settings.md#BKMK_DisableRemote)  
  
-   [メディアライブラリ名を設定する](Change-Media-Streaming-Settings.md#BKMK_LibraryName)  
  
-   [ビデオストリーミングの品質を設定する](Change-Media-Streaming-Settings.md#BKMK_StreamingQuality)  
  
-   [プログラムによってメディアストリーミングを有効または無効にする](Change-Media-Streaming-Settings.md#BKMK_Program)  
  
##  <a name="hide-remote-media-streaming-add-in"></a><a name="BKMK_DisableRemote"></a>リモートメディアストリーミングアドインを非表示にする  
 リモート メディア ストリーミング アドインを非表示にするには、レジストリのエントリを追加します。  
  
#### <a name="to-hide-the-remote-media-streaming-add-in"></a>リモート メディア ストリーミング アドインを非表示にするには  
  
1.  サーバーで、カーソルを画面の右上隅に移動して、 **[検索]** をクリックします。  
  
2.  **[検索]** ボックスに「**regedit**」と入力して、**Regedit** アプリケーションをクリックします。  
  
3.  左側のウィンドウで、次のレジストリ エントリまで展開します。  
  
     **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\RemoteAccess\DisabledAddIns**  
  
4.  **[DisabledAddIns]** を右クリックし、 **[新規]** をクリックし、 **[DWORD 値]** をクリックします。  
  
5.  新しい値に「**497796c6-9cc7-43be-aa26-4e6b5695370d**」 (リモート メディア ストリーミング アドインの識別子) と入力して、**Enter** キーを押します。  
  
6.  値を右クリックして、 **[変更]** をクリックします。  
  
7.  値データに「**1**」と入力し、 **[OK]** をクリックします。  
  
##  <a name="set-the-media-library-name"></a><a name="BKMK_LibraryName"></a>メディアライブラリ名を設定する  
 Windows Server Solutions SDK のクラスを使用して、メディア ライブラリ名を設定できます。 メディア ライブラリ名を設定するには、**Microsoft.WindowsServerSolutions.MediaStreaming** 名前空間の **MediaStreamingManager** クラスの **SetMediaLibraryName** メソッドを使用します。 次の例では、メディア ライブラリ名を設定する方法を示します。  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
string mediaLibraryName = Guid.NewGuid().ToString("B");   
mediaStreamingManager.SetMediaLibraryName(mediaLibraryName);  
  
```  
  
 詳細については、 [Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)を参照してください。  
  
##  <a name="set-video-streaming-quality"></a><a name="BKMK_StreamingQuality"></a>ビデオストリーミングの品質を設定する  
 ビデオ ストリーミングの品質を設定するには、WinSAT CPU スコアを取得し、WinSAT スコア情報を含む .xml ファイルを作成およびインストールします。 初期構成を実行する前に WinSAT スコア情報を含む .xml ファイルをインストールすると、ビデオ品質の設定のためのユーザー インターフェイスがお客様の画面に表示されなくなります。 詳細については、「[サーバーでの WinSAT スコアの設定](Set-the-WinSAT-Score-on-the-Server.md)」を参照してください。  
  
##  <a name="programmatically-enable-or-disable-media-streaming"></a><a name="BKMK_Program"></a>プログラムによってメディアストリーミングを有効または無効にする  
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
  
## <a name="see-also"></a>参照  
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)