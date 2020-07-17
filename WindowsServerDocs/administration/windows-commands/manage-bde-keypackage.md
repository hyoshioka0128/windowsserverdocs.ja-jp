---
title: manage-bde keypackage
description: ドライブのキーパッケージを生成する manage-bde keypackage コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c631ef10-2a2f-4541-8578-292f2d4e9e80
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4bdbd9bb46b75e7dc87cae1cd6e9b3a101ff91ff
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928566"
---
# <a name="manage-bde-keypackage"></a>manage-bde keypackage

ドライブのキー パッケージを生成します。 キーパッケージは、破損したドライブを修復するために修復ツールと組み合わせて使用できます。

## <a name="syntax"></a>構文

```
manage-bde -keypackage [<drive>] [-ID <keyprotectoryID>] [-path <pathtoexternalkeydirectory>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<drive>` | コロンの後にドライブ文字を表します。 |
| -ID | キープロテクターと、この ID 値で指定した識別子を使用して、キーパッケージを作成します。 **ヒント:** キーパッケージを作成するドライブ文字と共に**manage-bde – protectors – get**コマンドを使用して、ID 値として使用する使用可能な guid の一覧を取得します。 |
| -path | 作成したキーパッケージを保存する場所を指定します。 |
| -computername | manage-bde.exe が別のコンピューターの BitLocker 保護を変更するために使用されることを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | 表示は、コマンド プロンプトでヘルプを完了します。 |

### <a name="examples"></a>例

GUID で識別されるキープロテクターに基づいて C ドライブのキーパッケージを作成し、キーパッケージを F:\Folder に保存するには、次のように入力します。

```
manage-bde -keypackage C: -id {84E151C1...7A62067A512} -path f:\Folder
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [manage-bde コマンド](manage-bde.md)
