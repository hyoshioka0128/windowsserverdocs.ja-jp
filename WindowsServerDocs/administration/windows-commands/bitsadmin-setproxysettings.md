---
title: bitsadmin setproxysettings
description: Windows コマンド」のトピック**bitsadmin setproxysettings** -指定したジョブのプロキシ設定を指定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3503aab55f5650cb9283ce8a9f1a17359bfd48b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825593"
---
# <a name="bitsadmin-setproxysettings"></a>bitsadmin setproxysettings



指定したジョブのプロキシ設定を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetProxySettings <Job> <Usage> [List] [Bypass]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|使用方法|次のいずれかの値です。</br>-PRECONFIG-所有者の Internet Explorer の既定値を使用します。</br>-NO_PROXY — プロキシ サーバーを使用しません。</br>-オーバーライド-明示的なプロキシのリストを使用し、リストをバイパスします。 プロキシとプロキシ バイ パス一覧が従う必要があります。</br>-AUTODETECT: プロキシ設定を自動的に検出します。|
|一覧|際に使用される、*使用状況*パラメーターの上書きに設定されて、使用するプロキシ サーバーのコンマ区切りの一覧が含まれています。|
|バイパス|際に使用される、*使用状況*パラメーターの上書きを設定する: スペースで区切られた一覧を含むのホスト名または IP アドレス、またはその両方を対象の転送はプロキシを経由してルーティングします。 これは、 **\<ローカル >** を同じ LAN 上のすべてのサーバーを参照してください。 NULL 値または""を空のプロキシ バイ パス一覧の使用可能性があります。|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのプロキシ設定を設定する*myDownloadJob*します。

```
C:\>bitsadmin /SetProxySettings myDownloadJob PRECONFIG
```

その他の例に示します。

```
bitsadmin /setproxysettings myDownloadJob NO_PROXY
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1:80 ""
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1,proxy2,proxy3 NULL
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)