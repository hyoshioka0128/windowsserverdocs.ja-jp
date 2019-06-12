---
title: shrink
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec87cc7c-9846-465e-a10d-4ee10db4f4e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09cc9ce7beebc04a0a45cd93c2b0da25c5a1a49e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441265"
---
# <a name="shrink"></a>shrink

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Diskpart 圧縮コマンドは、指定した量によって、選択したボリュームのサイズを縮小します。 このコマンドでは、ボリュームの最後に、未使用の領域から使用可能な空きディスク領域を作成します。

## <a name="syntax"></a>構文
```
shrink [desired=<n>] [minimum=<n>] [nowait] [noerr]
shrink querymax [noerr]
```
## <a name="parameters"></a>パラメーター

|  パラメーター  |                                                                                             説明                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| desired=<n> |                                                     メガバイト (MB)、ボリュームのサイズを小さく領域の必要な量を指定します。                                                     |
| 最小値 =<n> |                                                           (Mb) ではボリュームのサイズを小さくには、領域の最小容量を指定します。                                                           |
|  querymax   |                       ボリュームを削減できます (mb) の領域の最大量を返します。 アプリケーションは、ボリュームを現在アクセスしている場合、この値を変更できます。                        |
|   nowait    |                                                       圧縮処理が進行中のときにすぐに返されるコマンドを強制します。                                                        |
|    noerr    | スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="remarks"></a>注釈
- NTFS ファイル システムでフォーマットされている場合またはファイル システムがあるない場合にのみ、ボリュームのサイズを小さくことができます。
- このコマンドは、ベーシック ボリュームとシンプル ボリュームまたはスパン ダイナミック ボリュームは機能します。
- 必要な容量が指定されていない場合、ボリューム値下げされる予定最小限 (選択した場合のみ)。
- 最小量が指定されていない場合、ボリュームはだけ値下げされる、必要な (選択した場合のみ)。
- 最低限でも、必要な時間が指定されている場合、ボリュームが値下げされる可能な限りです。
- 最小量を指定し、十分な空き領域が、コマンドは失敗します。
- この操作を成功させるのには、ボリュームを選択してください。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。
- このコマンドは、相手先ブランド供給業者 (OEM) パーティション、拡張ファームウェア インターフェイス (EFI) システム パーティション、または回復パーティションについては動作しません。
  ## <a name="BKMK_examples"></a>例
  選択したボリュームのサイズを減らすためを 250 および 500 件のメガバイト数の間で最大の可能な量には、次のように入力します。
  ```
  shrink desired=500 minimum=250
  ```
  削減されることができます、ボリュームを mb 単位の最大数を表示するには、次のように入力します。
  ```
  shrink querymax
  ```

[複数のパーティションにサイズ変更](https://technet.microsoft.com/library/hh848680.aspx)
