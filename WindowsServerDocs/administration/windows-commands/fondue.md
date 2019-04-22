---
title: fondue
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc4467f6-ddbb-4d6d-b51e-5a50a957b8c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 09708c239b5399f3284c42877970443cc2605cbe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817153"
---
# <a name="fondue"></a>fondue

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows のオプション機能ことにより、Windows Update またはグループ ポリシーで指定された別のソースから必要なファイルをダウンロードします。 機能のマニフェスト ファイルは、Windows イメージに既にインストールする必要があります。 
## <a name="syntax"></a>構文
```
fondue.exe /enable-feature:<feature_name> [/caller-name:<program_name>] [/hide-ux:{all | rebootRequest}]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/enable-feature: <*feature_name*>|有効にする Windows の省略可能な機能の名前を指定します。 コマンド ラインあたり 1 つの機能を有効にすることができますのみです。 複数の機能を有効にするには、各機能の fondue.exe を使用します。|
|/caller-name:<*program_name*>|スクリプトまたはバッチ ファイルから fondue.exe を呼び出すときに、プログラムまたはプロセス名を指定します。 このオプションを使用して、エラーがある場合は、SQM レポートにプログラム名を追加することができます。|
|/hide-ux:{all &#124; rebootRequest}|使用**すべて**Windows Update にアクセスする進行状況とアクセス許可の要求を含む、ユーザーにすべてのメッセージを非表示にします。 アクセス許可が必要な場合、操作は失敗します。<br /><br />使用**rebootRequest**のみコンピューターを再起動する許可を求めるユーザー メッセージを非表示にします。 コントロールに要求が再起動されるスクリプトがある場合は、このオプションを使用します。|
## <a name="BKMK_Examples"></a>例
Microsoft .NET Framework 3.5 を有効にするには、次のように入力します。
```
fondue.exe /enable-feature:NETFX3
```
Microsoft .NET Framework 3.5 を有効にするには、は、SQM レポートにプログラム名を追加し、型、ユーザーにメッセージが表示されません。
```
fondue.exe /enable-feature:NETFX3 /caller-name:Admin.bat /hide-ux:all
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
## <a name="see-also"></a>関連項目
[Microsoft .NET Framework 3.5 展開に関する考慮事項](https://go.microsoft.com/fwlink/?LinkId=248869)
