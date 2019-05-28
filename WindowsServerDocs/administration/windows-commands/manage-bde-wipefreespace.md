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
ms.openlocfilehash: 7cf99a9124f78189de223018608d9864e51d7897
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564692"
---
# <a name="manage-bde-wipefreespace"></a>manage-bde:WipeFreeSpace



空間に存在するデータの断片を削除するボリュームに空き領域を消去します。 このコマンドを"使用済み領域のみ"の暗号化メソッドを使用して暗号化されたボリュームで実行されている同じレベルの「フル ボリューム暗号化」の暗号化方法として、保護を提供します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde -WipeFreeSpace|-w [<Drive>] [-Cancel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
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
次の例を使用して、 **-w**コマンドと、 **-キャンセル**パラメーター C ドライブの空き領域のクリーン インストールをキャンセルするには
```
manage-bde -w -Cancel C:
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)