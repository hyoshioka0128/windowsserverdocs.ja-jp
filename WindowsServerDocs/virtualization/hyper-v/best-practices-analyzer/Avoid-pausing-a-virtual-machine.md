---
title: 仮想マシンの一時停止を避ける
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 930f927c-e414-4a36-9786-028941e886e4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 6799795ae383fd0522ce0b35eba0443ae536b0dd
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969999"
---
# <a name="avoid-pausing-a-virtual-machine"></a>仮想マシンの一時停止を避ける

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題

*このサーバーには、一時停止状態の仮想マシンが1つ以上あります。*

## <a name="impact"></a>影響

*使用可能なメモリの量によっては、追加の仮想マシンを実行できない場合があります。*

一時停止した仮想マシンは、割り当てられたメモリを解放しません。つまり、他の仮想マシンを起動するためにメモリが使用できないことを意味します。

## <a name="resolution"></a>解決方法

*これが意図的なものである場合は、それ以上の操作は必要ありません。それ以外の場合は、これらの仮想マシンを再開するか、シャットダウンすることを検討してください。*

#### <a name="use-hyper-v-manager-to-resume-the-virtual-machine"></a>Hyper-v マネージャーを使用して仮想マシンを再開する

1.  Hyper-V マネージャーを開きます。 (サーバーマネージャーの [**ツール**] メニューの [ **hyper-v マネージャー**] をクリックします)。

2.  [ **Virtual Machines** ] ボックスの一覧から、状態が [**一時停止**] になっている仮想マシンを見つけます。

    > [!IMPORTANT]
    > "**一時停止-重大**" の状態は、その仮想マシンの物理記憶域に残っている空き領域がほとんどない場合に発生します。 この状態でバーチャルマシンを再開する前に、物理記憶域の空き領域を解放してください。

3.  各仮想マシン名を右クリックし、[**再開**] をクリックします。 これで、仮想マシンが実行状態に戻ります。 その後、仮想マシンをシャットダウンする場合は、仮想マシンをもう一度右クリックし、[**シャットダウン**] を選択します。

#### <a name="use-windows-powershell-to-resume-the-virtual-machine"></a>Windows PowerShell を使用して仮想マシンを再開する

この操作は、ホスト上のすべての仮想マシンを取得した後、フィルターとパイプラインを使用して1つのコマンドで実行できます。 型:

```
get-vm | where state -eq 'paused' | resume-vm
```



