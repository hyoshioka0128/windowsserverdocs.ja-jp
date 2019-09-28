---
title: ホスト型キャッシュを移動およびサイズ変更する (省略可能)
description: このガイドでは、Windows Server 2016 と Windows 10 を実行するコンピューターに、ホスト型キャッシュモードで BranchCache を展開する手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: bb0eb349-914d-4596-9140-d3aae7597d55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0b0e3b6b490dead32071d99becccd9dca937f1f3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406368"
---
# <a name="move-and-resize-the-hosted-cache-optional"></a>ホスト型キャッシュの移動とサイズ変更 \(Optional @ no__t-1

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この手順を使用すると、ホスト型キャッシュを目的のドライブとフォルダーに移動したり、ホスト型キャッシュサーバーがホスト型キャッシュに使用できるディスク領域の量を指定したりすることができます。

この手順は省略可能です。 既定のキャッシュの場所 \(% windir% \\ServiceProfiles @ no__t-2NetworkService @ no__t-3AppData @ no__t-4Local @ no__t-5PeerDistPub @ no__t-6 と size (ハードディスクの合計容量の 5%) が展開に適している場合、変更する必要があります。

この手順を実行するには、Administrators グループのメンバーである必要があります。

### <a name="to-move-and-resize-the-hosted-cache"></a>ホスト型キャッシュの移動とサイズ変更を行うには

1. 管理者特権で Windows PowerShell を開きます。

2. 次のコマンドを入力して、ホスト型キャッシュをローカルコンピューター上の別の場所に移動し、enter キーを押します。

    > [!IMPORTANT]
    > 次のコマンドを実行する前に、– Path や– MoveTo などのパラメーター値を、配置に適した値に置き換えます。

    ``` 
    Set-BCCache -Path C:\datacache –MoveTo D:\datacache
    ``` 

3.  次のコマンドを入力して、ローカルコンピューター上のホスト型キャッシュのサイズを変更します (具体的には datacache \-)。 Enter キーを押します。

    > [!IMPORTANT]
    > 次のコマンドを実行する前に、\-Percentage などのパラメーター値を、配置に適した値に置き換えます。  

    ``` 
    Set-BCCache -Percentage 20
    ``` 

4.  ホスト型キャッシュサーバーの構成を確認するには、次のコマンドを入力し、enter キーを押します。

    ``` 
    Get-BCStatus
    ``` 

    コマンドの結果は、BranchCache インストールのすべての側面の状態を表示します。 次に、BranchCache の設定のいくつかと、各項目の正しい値を示します。

    -   DataCache |CacheFileDirectoryPath:SetBCCache コマンドの– MoveTo パラメーターで指定した値と一致するハードディスクの場所が表示されます。 たとえば、値 D: @no__t を指定した場合、その値はコマンドの出力に表示されます。

    -   DataCache |MaxCacheSizeAsPercentageOfDiskVolume:SetBCCache コマンドの–パーセントパラメーターで指定した値と一致する数値が表示されます。 たとえば、値20を指定した場合、その値はコマンドの出力に表示されます。

このガイドを使用するには、「[ホスト型キャッシュサーバー &#40;でのコンテンツの事前&#41;ハッシュと事前読み込み](7-Bc-Prehash-Preload.md)」を参照してください (省略可能)。