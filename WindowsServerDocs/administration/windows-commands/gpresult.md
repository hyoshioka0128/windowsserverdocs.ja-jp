---
title: gpresult
description: Gpresult コマンドのリファレンストピック。リモートユーザーとコンピューターのポリシーの結果セット (RSoP) 情報を表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dfaa3adf-2c83-486c-86d6-23f93c5c883c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e88a75a15168baaf2e49ca08ff20d3a8ffb5620c
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818862"
---
# <a name="gpresult"></a>gpresult

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートユーザーとコンピューターのポリシーの結果セット (RSoP) 情報を表示します。 ファイアウォール経由でリモートターゲットコンピューターの RSoP レポートを使用するには、ポートで受信ネットワークトラフィックを有効にするファイアウォール規則が必要です。

## <a name="syntax"></a>構文

```
gpresult [/s <system> [/u <username> [/p [<password>]]]] [/user [<targetdomain>\]<targetuser>] [/scope {user | computer}] {/r | /v | /z | [/x | /h] <filename> [/f] | /?}
```

> [!NOTE]
> **/?** を使用する場合を除き、出力オプション、 **/r**、 **/v**、 **/z**、 **/x**、または **/h**を含める必要があります。

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /s`<system>` | 名前またはリモート コンピューターの IP アドレスを指定します。 バックスラッシュは使用しないでください。 既定はローカル コンピュータです。 |
| /u`<username>` | 指定されたユーザーの資格情報を使用してコマンドを実行します。 既定のユーザーは、コマンドを発行するコンピューターにログオンしているユーザーです。 |
| /p`[<password>]` | **/U**パラメーターに指定されているユーザーアカウントのパスワードを指定します。 **/P**を省略した場合、 **gpresult**はパスワードの入力を求めます。 **/P**パラメーターは、 **/x**または **/h**と共に使用することはできません。 |
| /user`[<targetdomain>\]<targetuser>]` | RSoP データを表示するリモートユーザーを指定します。 |
| /scope`{user | computer}` | ユーザーまたはコンピューターの RSoP データを表示します。 **/Scope**を省略した場合、 **gpresult**はユーザーとコンピューターの両方の RSoP データを表示します。 |
| `[/x | /h] <filename>` | は、 *filename*パラメーターで指定されたファイル名を使用して、レポートを XML (**/x**) 形式または HTML 形式 (**/h**) 形式で保存します。 **/U**、 **/p**、 **/r**、 **/v**、または **/z**と共に使用することはできません。 |
| /f | **/X**または **/h**オプションで指定されたファイル名を強制的に**gpresult**に上書きします。 |
| /r | RSoP の概要データを表示します。 |
| /v | 詳細なポリシー情報を表示します。 これには、優先順位1で適用された詳細設定が含まれます。 |
| /z | グループポリシーに関する利用可能なすべての情報を表示します。 これには、1以上の優先順位で適用された詳細設定が含まれます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- グループポリシーは、組織内のユーザーとコンピューターに対してプログラム、ネットワークリソース、およびオペレーティングシステムがどのように動作するかを定義および制御するための主要な管理ツールです。 Active directory 環境では、グループポリシーは、サイト、ドメイン、または組織単位のメンバーシップに基づいてユーザーまたはコンピューターに適用されます。

- 重複したポリシー設定を任意のコンピューターまたはユーザーに適用できるため、グループポリシー機能によって、ユーザーがログオンしたときに生成されるポリシー設定のセットが生成されます。 **Gpresult**コマンドを実行すると、ユーザーがログオンしたときに、指定したユーザーのコンピューターに適用されたポリシー設定の結果セットが表示されます。

- **/V**および **/z**では大量の情報が生成されるため、出力をテキストファイルにリダイレクトすると便利です (たとえば、 `gpresult/z >policy.txt` )。

### <a name="examples"></a>例

リモートユーザーのみの RSoP データを取得するには、 *maindom\hiropln* *p@ssW23* コンピューターの*srvmain*にあるパスワードを使用して、次のように入力します。

```
gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /scope user /r
```

グループポリシーに関する利用可能なすべての情報を、 *maindom\hiropln*という名前のファイルに保存するに*は、* コンピューターの *p@ssW23* *srvmain*に、次のように入力します。

```
gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /z > policy.txt
```

ログオンしているユーザーの RSoP データを表示するには、 *maindom\hiropln* *p@ssW23* コンピューターの*srvmain*に、次のように入力します。

```
gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /r
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
