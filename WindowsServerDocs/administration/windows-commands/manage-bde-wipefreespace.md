---
title: manage-bde WipeFreeSpace
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b8d83a2a-c5c8-4019-9041-23d1d6abf282
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8750094e7357a3aefa307d24abd1470fbf8d2a71
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867173"
---
# <a name="manage-bde-wipefreespace"></a>manage-bde:WipeFreeSpace



空間に存在するデータの断片を削除するボリュームに空き領域を消去します。 "使用領域のみを使用して暗号化されたボリュームにこのコマンドを実行しますか? 暗号化方法は、同じレベルの"フル ボリューム暗号化として保護を提供します。? 暗号化方法。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde –WipeFreeSpace|-w [<Drive>] [-Cancel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >|続けて、コロン、ボリューム GUID パス、または、マウントされたボリュームのドライブ文字を表します。|
|-[キャンセル]|プロセスでは、空き領域のクリーン インストールをキャンセルします。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 使用することも **- cn**としてこのコマンドの簡易版です。|
|\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|ヘルプの簡単なコマンド プロンプトが表示されます。|
|--help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="BKMK_Examples"></a>例

次の例を使用して、 **-w** を作成するコマンドは、C ドライブの空き領域をワイプ
```
manage-bde -w C:
```
使用して、次の例に示す、 **-w** コマンドと組み合わせて、 **– キャンセル** C ドライブの空き領域のクリーン インストールをキャンセルするパラメーター
```
manage-bde -w -Cancel C:
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)