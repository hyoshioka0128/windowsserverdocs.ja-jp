---
title: manage-bde KeyPackage
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c631ef10-2a2f-4541-8578-292f2d4e9e80
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8fb49ce8fbe4be076151b203560e62f44a78c9d4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886903"
---
# <a name="manage-bde-keypackage"></a>manage-bde:KeyPackage



ドライブのキー パッケージを生成します。 キー パッケージは、破損したドライブを修復する修復ツールと組み合わせて使用できます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde -KeyPackage [<Drive>] [-ID <KeyProtectoryID>] [-path <PathToExternalKeyDirectory>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >|コロンの後にドライブ文字を表します。|
|-ID|この ID 値で指定された識別子を持つキー保護機能を使用してキー パッケージを作成します。|
|-path|作成されたキー パッケージを保存する場所です。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 使用することも **- cn**としてこのコマンドの簡易版です。|
|\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|ヘルプの簡単なコマンド プロンプトが表示されます。|
|--help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="BKMK_Examples"></a>例

次の例を使用して、 **- KeyPackage** F:\Folder にキー パッケージを保存して、GUID によって識別されるキー保護機能に基づく C ドライブのキー パッケージを作成するコマンド。
```
manage-bde -KeyPackage C: -id {84E151C1...7A62067A512} -path "f:\Folder"
```

> [!TIP]
> 使用して、 **、manage-bde – プロテクター-取得**ID 値として使用する使用可能な Guid の一覧を取得するためにキー パッケージを作成するドライブ文字とします。

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)