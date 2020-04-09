---
title: manage-bde KeyPackage
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c631ef10-2a2f-4541-8578-292f2d4e9e80
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a53edd060cb8c7a7a52e86130b2136893a42150
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840105"
---
# <a name="manage-bde-keypackage"></a>manage-bde: KeyPackage



ドライブのキー パッケージを生成します。 キーパッケージは、破損したドライブを修復するために修復ツールと組み合わせて使用できます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde -KeyPackage [<Drive>] [-ID <KeyProtectoryID>] [-path <PathToExternalKeyDirectory>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >|コロンの後にドライブ文字を表します。|
|-ID|この ID 値で指定した識別子を使用して、キープロテクターを使用してキーパッケージを作成します。|
|-path|作成されたキーパッケージを保存する場所。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a><a name=BKMK_Examples></a>例

次の例では、 **-KeyPackage**コマンドを使用して、GUID で識別されるキープロテクターに基づいて C ドライブのキーパッケージを作成し、キーパッケージを F:\Folder. に保存する方法を示します。
```
manage-bde -KeyPackage C: -id {84E151C1...7A62067A512} -path f:\Folder
```

> [!TIP]
> ID 値として使用する使用可能な Guid の一覧を取得するには、**管理-bde –プロテクター–** キーパッケージを作成するドライブ文字と共に get を使用します。

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)