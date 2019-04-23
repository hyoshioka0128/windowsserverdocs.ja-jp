---
title: Get AllServers コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe2e3c69-8f2e-457d-af55-d249ebf70f53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 080836e406b329cf8c15f95ef6afc99973bb3e4d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853093"
---
# <a name="using-the-get-allservers-command"></a>Get AllServers コマンドを使用してください。



すべての Windows 展開サービス サーバーに関する情報を取得します。

> [!NOTE]
> このコマンドは、期間を延長環境内で多くの Windows 展開サービス サーバーがある場合、または、サーバーのリンクのネットワーク接続速度が遅い場合の所要時間をかかる場合があります。

## <a name="syntax"></a>構文

```
WDSUTIL [Options] /Get-AllServers /Show:{Config | Images | All} [/Detailed] [/Forest:{Yes | No}]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/Show:{Config | 画像 | すべて}|返される情報の種類を指定します。</br>-   **Config**サーバー構成情報を返します。</br>-   **イメージ**サーバー上のイメージ グループ、ブート イメージ、およびインストール イメージに関する情報を返します。</br>-   **すべて**サーバーの構成とイメージの情報を返します。|
|[/詳細]|組み合わせて使用すると、 **/Show:Images** または **/Show:All**, 、すべてのイメージの各イメージからメタデータを返します。 場合、 **詳細/** オプションを指定しない場合、既定の動作は、イメージの名前、説明、およびファイル名を返す。|
|[]、[フォレスト: {[はい] | No}]|フォレスト全体またはローカル ドメインの情報を返すかどうかを指定します。 このオプションの値が指定されていない場合、既定の動作は、ローカル ドメイン内のサーバーを返すには。|

## <a name="BKMK_examples"></a>例

すべてのサーバーに関する情報を表示するには、次のように入力します。
```
WDSUTIL /Get-AllServers /Show:Config
```
すべてのサーバーに関する詳細情報を表示するには、次のように入力します。
```
WDSUTIL /Verbose /Get-AllServers /Show:All /Detailed /Forest:Yes
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)