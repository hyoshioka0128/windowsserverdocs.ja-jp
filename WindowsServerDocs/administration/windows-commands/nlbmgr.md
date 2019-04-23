---
title: nlbmgr
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 89cb8590-b7cf-4a27-89fa-0fa62ea1a1ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ed11e702aeae66458f888e454c1bc1d1bc22630
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887083"
---
# <a name="nlbmgr"></a>nlbmgr

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ネットワーク負荷分散マネージャーを使用して、構成して、1 台のコンピューターから、ネットワーク負荷分散クラスターとすべてのクラスター ホストを管理し、他のホストにクラスターの構成をレプリケートすることもできます。 ネットワーク負荷分散マネージャーを開始するには、コマンドを使用してコマンドラインから**nlbmgr.exe**にインストールされる、 **\system32**フォルダー。
## <a name="syntax"></a>構文
```
nlbmgr [/help] [/noping] [/hostlist <filename>] [/autorefresh <interval>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/help|コマンド プロンプトにヘルプを表示します。|
|/noping|ネットワーク負荷分散マネージャーが Windows Management Instrumentation (WMI) を介してパートナーに連絡する前に、ホストに対して ping を実行するを防ぎます。 すべての利用可能なネットワーク アダプターで、インターネット制御メッセージ プロトコル (ICMP) を無効にした場合は、このオプションを使用します。 ネットワーク負荷分散マネージャーがご利用いただけませんホストに接続しようとすると、このオプションを使用する場合に遅延が発生するされます。|
|/hostlist <filename>|ネットワーク負荷分散マネージャーにファイル名で指定されたホストを読み込みます。|
|/autorefresh <interval>|ネットワーク負荷分散マネージャーのホストとクラスターの情報を更新すると、すべて<interval>秒。 間隔が指定されていない場合は 60 秒ごとに情報が更新されます。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)

