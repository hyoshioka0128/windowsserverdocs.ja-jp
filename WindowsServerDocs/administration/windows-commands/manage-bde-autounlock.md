---
title: manage-bde 自動ロック解除
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 063528bf-d235-4b44-887a-52a7d983e01a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 929469ad3d4bd8b3a76c3681a5f24424ba6d99df
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820722"
---
# <a name="manage-bde-autounlock"></a>manage-bde: 自動ロック解除



BitLocker で保護されたデータ ドライブの自動ロック解除を管理します。

## <a name="syntax"></a>構文

```
manage-bde -autounlock [{-enable|-disable|-clearallkeys}] <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]

```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-を有効にします。|データ ドライブの自動ロック解除を使用できます。|
|-を無効にします。|データ ドライブの自動ロック解除を無効にします。|
|-clearallkeys|オペレーティング システム ドライブに格納されているすべての外部キーを削除します。|
|\<ドライブ>|コロンの後にドライブ文字を表します。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a>例

**-自動ロック解除**コマンドを使用して、データドライブ E の自動ロック解除を有効にする方法を示します。
```
manage-bde –autounlock -enable E:
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)