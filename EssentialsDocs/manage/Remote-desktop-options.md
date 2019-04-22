---
title: リモート デスクトップのオプション
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51076946-ea9b-4ac7-9a6e-d6023816b97d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: bbf7f258b2904732ab2e605d1eb3ea6bd2d306be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818313"
---
# <a name="remote-desktop-options"></a>リモート デスクトップのオプション
 
  
## <a name="connection-speed"></a>接続速度  
 リモート Web アクセスを使用したネットワーク コンピューターへの接続の速度によって、ホスト コンピューターで使用できるデスクトップ オプションが決定します。 次の表は、リモート Web アクセス経由でリモート コンピューターに接続する速度によって、どのデスクトップ オプションが使用できるかを示したものです。  
  
||||||  
|-|-|-|-|-|  
||低速モデム (28.8 Kbps)|高速モデム (56 Kbps) (既定)|ブロードバンド (128 Kbps ～ 1.5 Mbps)|ローカル エリア ネットワーク (1.5 Mbps 以上)|  
|デスクトップの背景|いいえ|いいえ|X|〇|  
|フォント スムージング|いいえ|いいえ|X|〇|  
|デスクトップ コンポジション|いいえ|X|〇|〇|  
|ドラッグ中にウィンドウの内容を表示する|いいえ|X|〇|〇|  
|メニューとウィンドウのアニメーション|X|X|〇|〇|  
|テーマ|X|〇|〇|〇|  
|ビットマップのキャッシュ|〇|〇|〇|〇|  
  
## <a name="screen-size"></a>画面のサイズ  
 このオプションは、リモート アクセス Web サイトからリモート コンピューターに接続するときに、ローカル コンピューターで開かれるウィンドウのサイズを決定します。 ウィンドウのサイズはピクセルで表されます。  
  
> [!NOTE]
>  サーバーに接続するとき、ダッシュボードが開きます。 ダッシュボードの既定のサイズは 1024 x 741 で、サイズは変更可能です。  
  
-   全画面表示 (複数のモニター)  
  
-   1280 x 720  
  
-   1024 x 768  
  
-   800 x 600  
  
-   640 x 480  
  
## <a name="enable-the-remote-computer-to-print-to-my-local-printer"></a>リモート コンピューターからローカル プリンターに印刷できるようにする  
 既定で有効になっています。 このオプションでは、ローカル コンピューターに接続されているプリンターにリモート コンピューターから印刷できます。  
  
## <a name="play-sounds-from-the-remote-computer"></a>リモート コンピューターから音声を再生する  
 既定で有効になっています。 このオプションでは、ローカル コンピューターのシステム サウンドなどのサウンドをリモート コンピューターから再生できます。  
  
## <a name="enable-copy-and-paste-between-the-remote-computer-and-the-local-computer"></a>リモート コンピューターとローカル コンピューター間のコピーと貼り付けを有効にする  
 既定では有効になっていません。 このオプションでは、ローカル コンピューター上の 1 つの場所から別の場所にコピー、貼り付けするのと同じように、リモート コンピューターとローカル コンピューター間でファイルのコピーと貼り付けができるようになります。  
  
## <a name="enable-the-remote-computer-to-access-drives-on-my-local-computer"></a>リモート コンピューターからローカル コンピューターのドライブにアクセスできるようにする  
 既定では有効になっていません。 このオプションでは、ローカル コンピューターに接続されているハード ディスク ドライブ上のファイルやフォルダーに、リモート コンピューターからアクセスすることができます。  
  
## <a name="see-also"></a>関連項目  
  
-   [リモート Web アクセスを管理します。](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [リモート Web アクセスを使用します。](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)
