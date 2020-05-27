---
title: unlodctr
description: Unlodctr のリファレンストピックでは、サービスまたはデバイスドライバーのパフォーマンスカウンターの名前と説明テキストをシステムレジストリから削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fc8aa6f0-c1d9-47ea-937a-28152148e774
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8551b6fc76984b06f28bdda92dcd63791721ec90
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821292"
---
# <a name="unlodctr"></a>unlodctr

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サービスまたはデバイスドライバーの**パフォーマンスカウンター**名と**説明**テキストをシステムレジストリから削除します。

## <a name="syntax"></a>構文
```
Unlodctr <DriverName>
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|\<ドライバーの>|Windows Server 2003 レジストリから、ドライバーまたはサービスのパフォーマンスカウンターの名前の設定と説明のテキストを削除し <DriverName> ます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
> [!WARNING]
> レジストリを正しく編集しないと、システムが正常に動作しなくなる場合があります。 レジストリを変更する前に、コンピューター上の重要なデータのバックアップを作成する必要があります。

入力する情報にスペースが含まれる場合は、テキストを囲む引用符を使用して (たとえば、 <DriverName>)。

## <a name="examples"></a>例
Simple Mail Transfer Protocol (SMTP) サービスの現在のパフォーマンスレジストリ設定とカウンターの説明テキストを削除するには、次の手順を実行します。
```
unlodctr SMTPSVC
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)

