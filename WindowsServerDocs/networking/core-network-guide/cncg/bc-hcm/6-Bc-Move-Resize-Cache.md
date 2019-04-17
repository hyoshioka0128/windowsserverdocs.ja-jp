---
title: 移動し、(省略可能) ホスト型キャッシュのサイズを変更します。
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache を展開するの説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: bb0eb349-914d-4596-9140-d3aae7597d55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2a3ed1d6de1281575b33cdf75a5970d2ed033085
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="move-and-resize-the-hosted-cache-optional"></a>移動し、ホスト型キャッシュ \(Optional\) のサイズを変更します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ホスト型キャッシュをドライブと、必要に応じてフォルダーに移動して、ホスト型キャッシュ サーバーがホスト型キャッシュを使用できるディスク領域の量を指定するには、この手順を使用することができます。

この手順は省略可能です。 既定のキャッシュ場所 \(%windir%\\ServiceProfiles\\NetworkService\\AppData\\Local\\PeerDistPub\) と – されるハード_ディスクの合計領域の 5% – サイズが、展開に適切な場合は、それらを変更する必要はありません。

この手順を実行する管理者グループのメンバーがあります。

### <a name="to-move-and-resize-the-hosted-cache"></a>移動し、ホスト型キャッシュのサイズを変更するには

1. 管理者特権で Windows PowerShell を開きます。

2. 別の場所に、ローカル コンピューター上のホスト型キャッシュを移動するには、次のコマンドを入力し、し、ENTER キーを押します。

    > [!IMPORTANT]
    > 次のコマンドを実行する前に、– Path と – 移動などのパラメーターの値を展開に適切な値に置き換えます。

    ``` 
    Set-BCCache -Path C:\datacache –MoveTo D:\datacache
    ``` 

3.  ホストのサイズを変更するには、次のコマンドを入力キャッシュ – datacache 具体的には \ - ローカル コンピューター上です。 ENTER キーを押します。

    > [!IMPORTANT]
    > 次のコマンドを実行する前に、\-Percentage などのパラメーターの値を展開に適切な値に置き換えます。  

    ``` 
    Set-BCCache -Percentage 20
    ``` 

4.  ホスト型キャッシュ サーバーの構成を確認するには、次のコマンドを入力し、ENTER キーを押します。

    ``` 
    Get-BCStatus
    ``` 

    コマンドの結果は、BranchCache、インストールのすべての側面のステータスを表示します。 BranchCache の設定と各項目の正しい値の一部を次に示します。

    -   DataCache |CacheFileDirectoryPath: SetBCCache コマンドの – 移動パラメーターで指定した値と一致するハード_ディスクの場所を表示します。 たとえば、D:\\datacache 値を指定した場合は、コマンドの出力にその値が表示されます。

    -   DataCache |MaxCacheSizeAsPercentageOfDiskVolume: SetBCCache コマンドの – 割合パラメーターで指定した値と一致する数を表示します。 たとえば、20 の値を指定した場合は、コマンドの出力にその値が表示されます。

このガイドでは、続行するのを参照してください。 [Prehash しプリロードの [コンテンツのホスト型キャッシュ サーバー (&) #40";"オプション"&"#41 です。](7-Bc-Prehash-Preload.md).