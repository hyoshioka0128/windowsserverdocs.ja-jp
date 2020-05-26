---
title: nlbmgr
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 89cb8590-b7cf-4a27-89fa-0fa62ea1a1ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a055eb30984bd1832d84bce40607eb0722b175b2
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820852"
---
# <a name="nlbmgr"></a>nlbmgr

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ネットワーク負荷分散マネージャーを使用すると、ネットワーク負荷分散クラスターとすべてのクラスターホストを1台のコンピューターから構成して管理できます。また、クラスター構成を他のホストにレプリケートすることもできます。 コマンドラインからネットワーク負荷分散マネージャーを起動するには、 **systemroot\System32**フォルダーにインストールされているコマンド**nlbmgr**を使用します。
## <a name="syntax"></a>構文
```
nlbmgr [/help] [/noping] [/hostlist <filename>] [/autorefresh <interval>]
```
#### <a name="parameters"></a>パラメーター

|        パラメーター        |                                                                                                                                                                                                説明                                                                                                                                                                                                |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /help          |                                                                                                                                                                                   コマンド プロンプトにヘルプを表示します。                                                                                                                                                                                    |
|         /noping         | ネットワーク負荷分散マネージャが Windows Management Instrumentation (WMI) を使用してホストに接続する前に、ホストに ping を実行しないようにします。 使用可能なすべてのネットワークアダプターでインターネット制御メッセージプロトコル (ICMP) を無効にしている場合は、このオプションを使用します。 ネットワーク負荷分散マネージャーが、利用できないホストに接続しようとすると、このオプションを使用すると遅延が発生します。 |
|  /hostlist<filename>   |                                                                                                                                                                Filename で指定されたホストをネットワーク負荷分散マネージャーに読み込みます。                                                                                                                                                                 |
| /autorefresh<interval> |                                                                                                          ネットワーク負荷分散マネージャーによって、ホストとクラスターの情報が毎秒更新さ <interval> れます。 間隔が指定されていない場合、情報は60秒ごとに更新されます。                                                                                                          |
|           /?            |                                                                                                                                                                                   コマンド プロンプトにヘルプを表示します。                                                                                                                                                                                    |

## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)

