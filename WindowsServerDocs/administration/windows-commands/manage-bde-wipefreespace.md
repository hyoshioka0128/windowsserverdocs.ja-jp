---
title: manage-bde WipeFreeSpace 領域
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 35d5f5fe079485d35fa412502bec745a136fbce9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373783"
---
# <a name="manage-bde-wipefreespace"></a>manage-bde.exeWipeFreeSpace 領域



空間に存在するデータの断片を削除するボリュームに空き領域を消去します。 "使用領域のみ" の暗号化方法を使用して暗号化されたボリュームでこのコマンドを実行すると、"完全ボリューム暗号化" 暗号化方式と同じレベルの保護が提供されます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde -WipeFreeSpace|-w [<Drive>] [-Cancel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<Drive >|続けて、コロン、ボリューム GUID パス、または、マウントされたボリュームのドライブ文字を表します。|
|-[キャンセル]|プロセスでは、空き領域のクリーン インストールをキャンセルします。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<名前 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="BKMK_Examples"></a>例

次の例を使用して、 **-w** を作成するコマンドは、C ドライブの空き領域をワイプ
```
manage-bde -w C:
```
次の例では、- **w**コマンドと **-cancel**パラメーターを使用して、ドライブ C の空き領域のワイプをキャンセルする方法を示します。
```
manage-bde -w -Cancel C:
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)