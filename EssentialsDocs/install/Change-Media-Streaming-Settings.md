---
title: "メディア ストリーミング設定を変更します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="change-media-streaming-settings"></a>メディア ストリーミング設定を変更します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

複数のオプションを使用すると、メディア ストリーミング設定を変更します。 次のオプションを使用できます。  
  
-   [リモート メディア ストリーミング アドインを非表示にします。](Change-Media-Streaming-Settings.md#BKMK_DisableRemote)  
  
-   [メディア ライブラリ名を設定します。](Change-Media-Streaming-Settings.md#BKMK_LibraryName)  
  
-   [ビデオ ストリーミングの品質を設定します。](Change-Media-Streaming-Settings.md#BKMK_StreamingQuality)  
  
-   [プログラムによって有効またはメディア ストリーミングを無効にします。](Change-Media-Streaming-Settings.md#BKMK_Program)  
  
##  <a name="BKMK_DisableRemote"></a>リモート メディア ストリーミング アドインを非表示にします。  
 リモート メディア ストリーミング アドイン レジストリにエントリを追加することで非表示にすることができます。  
  
#### <a name="to-hide-the-remote-media-streaming-add-in"></a>リモート メディア ストリーミング アドインを非表示にするには  
  
1.  サーバーで、マウスを移動して、画面の右上隅とクリックして**検索**します。  
  
2.  **検索**ボックスに、入力**regedit**、クリックして、 **Regedit**アプリケーション。  
  
3.  左側のウィンドウでは、次のレジストリ エントリまで展開します。  
  
     **Hkey_local_machine \software\microsoft\windows Server\RemoteAccess\DisabledAddIns**  
  
4.  右クリック**DisabledAddIns**、] をポイント**新規**、] をクリックし、 **DWORD 値**します。  
  
5.  新しい値の次のように入力します。 **497796c6-9cc7-43be-aa26-4e6b5695370d**、リモート メディア ストリーミング アドインの識別子とキーを押します**Enter**します。  
  
6.  値を右クリックし、をクリックして**変更**します。  
  
7.  種類**1**値のデータ、およびクリック**OK**します。  
  
##  <a name="BKMK_LibraryName"></a>メディア ライブラリ名を設定します。  
 Windows Server Solutions SDK のクラスを使用して、メディア ライブラリ名を設定することができます。 使用することができます、メディア ライブラリ名を設定する、 **SetMediaLibraryName**方法、 **MediaStreamingManager**クラスを**Microsoft.WindowsServerSolutions.MediaStreaming**名前空間です。 次の例では、メディア ライブラリの名前を設定する方法を示します。  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
string mediaLibraryName = Guid.NewGuid().ToString("B");   
mediaStreamingManager.SetMediaLibraryName(mediaLibraryName);  
  
```  
  
 詳細については、次を参照してください。 [Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)します。  
  
##  <a name="BKMK_StreamingQuality"></a>ビデオ ストリーミングの品質を設定します。  
 ビデオ ストリーミングの品質 WinSAT CPU スコアの取得を作成し、WinSAT スコア情報を含む .xml ファイルのインストールを設定します。 WinSAT スコア情報を含む .xml ファイルが初期構成を実行する前にインストールされている顧客には、ビデオ品質の設定のユーザー インターフェイスは表示されない場合。 詳細については、次を参照してください。[サーバーの WinSAT スコアの設定](Set-the-WinSAT-Score-on-the-Server.md)します。  
  
##  <a name="BKMK_Program"></a>プログラムによって有効またはメディア ストリーミングを無効にします。  
 Windows Server Solutions SDK のクラスを使用してプログラムで有効または、メディア ストリーム配信を無効にすることができます。 有効または、メディア ストリーミングを無効にする、使用することができます、 **SetMediaStreamingEnabled**方法、 **MediaStreamingManager**クラスを**Microsoft.WindowsServerSolutions.MediaStreaming**名前空間です。 次のコード例は、メディア ストリーミングを有効にする方法を示します。  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(true);  
  
```  
  
 次のコード例は、メディア ストリーミングを無効にする方法を示します。  
  
```c#  
  
MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();  
mediaStreamingManager.SetMediaStreamingEnabled(false);  
```  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)