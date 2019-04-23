---
title: ホスト型キャッシュを移動およびサイズ変更する (省略可能)
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache の展開の説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: bb0eb349-914d-4596-9140-d3aae7597d55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cb75e06b5da8ff95fcf763b22c5160ea200035f3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853533"
---
# <a name="move-and-resize-the-hosted-cache-optional"></a>移動して、ホスト型キャッシュのサイズを変更\(オプション\)

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ホスト型キャッシュをドライブと、必要なフォルダーに移動し、ホスト型キャッシュのホスト型キャッシュ サーバーが使用できるディスク領域の量を指定するには、この手順を使用することができます。

この手順は省略可能です。 キャッシュの場所を既定の場合\(%windir%\\ServiceProfiles\\NetworkService\\AppData\\ローカル\\PeerDistPub\)とハード_ディスクの合計の 5% のサイズ。領域-適切な展開にはそれらを変更する必要はありません。

この手順を実行する管理者グループのメンバーがあります。

### <a name="to-move-and-resize-the-hosted-cache"></a>移動して、ホスト型キャッシュのサイズを変更するには

1. 管理者特権で Windows PowerShell を開きます。

2. ローカル コンピューターでは、ホスト型キャッシュを別の場所に移動するには、次のコマンドを入力し、ENTER キーを押します。

    > [!IMPORTANT]
    > 次のコマンドを実行する前に、– Path と – MoveTo などのパラメーター値を展開に適切な値に置き換えます。

    ``` 
    Set-BCCache -Path C:\datacache –MoveTo D:\datacache
    ``` 

3.  ホストのサイズを変更するには、次のコマンドを入力キャッシュ – datacache 具体的には\-ローカル コンピューター上です。 Enter キーを押します。

    > [!IMPORTANT]
    > 次のコマンドを実行する前に、パラメーター値のなど置換\-展開に適切な値を持つの割合。  

    ``` 
    Set-BCCache -Percentage 20
    ``` 

4.  ホスト型キャッシュ サーバーの構成を確認するには、次のコマンドを入力し、ENTER キーを押します。

    ``` 
    Get-BCStatus
    ``` 

    コマンドの結果は、BranchCache インストールのすべての側面の状態を表示します。 次に、BranchCache の設定および項目ごとに適切な値のいくつか示します。

    -   DataCache |CacheFileDirectoryPath:SetBCCache コマンドの – MoveTo パラメーターで指定した値に一致するハード_ディスクの場所が表示されます。 たとえば、d: の値を指定した\\datacache、値がコマンドの出力に表示されることです。

    -   DataCache |MaxCacheSizeAsPercentageOfDiskVolume:SetBCCache コマンドの – の割合パラメーターで指定した値に一致する番号が表示されます。 たとえば、20 の値を指定した場合は、コマンドの出力にその値が表示されます。

このガイドを続行する、次を参照してください。 [Prehash し、ホスト型キャッシュ サーバー上の事前読み込みコンテンツ&#40;(省略可能)&#41;](7-Bc-Prehash-Preload.md)します。