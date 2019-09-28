---
title: gpresult
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dfaa3adf-2c83-486c-86d6-23f93c5c883c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bb61911450ea8c0c68af0cf1a35c2f571810504b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375656"
---
# <a name="gpresult"></a>gpresult

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートユーザーとコンピューターのポリシーの結果セット (RSoP) 情報を表示します。
ファイアウォール経由でリモートターゲットコンピューターの RSoP レポートを使用するには、ポートで受信ネットワークトラフィックを有効にするファイアウォール規則が必要です。

## <a name="syntax"></a>構文

```
gpresult [/s <system> [/u <USERNAME> [/p [<PASSWOrd>]]]] [/user [<TARGETDOMAIN>\]<TARGETUSER>] [/scope {user | computer}] {/r | /v | /z | [/x | /h] <FILENAME> [/f] | /?}
```

## <a name="parameters"></a>パラメーター

> [!NOTE]
> **/?** を使用する場合を除き、出力オプションには、 **/r**、 **/v**、 **/z**、 **/x**、または **/h**を含める必要があります。

|                パラメーター                 |                                                                                                     説明                                                                                                      |
|------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              /s \<system @ no__t               |                                                  名前またはリモート コンピューターの IP アドレスを指定します。 円記号を使用しないでください。 既定はローカル コンピュータです。                                                   |
|             /u \<USERNAME @ no__t              |                                指定されたユーザーの資格情報を使用してコマンドを実行します。 既定のユーザーは、コマンドを発行するコンピューターにログオンしているユーザーです。                                 |
|            /p [\<PASSWOrd @ no__t-1]             |            **/U**パラメーターに指定されているユーザーアカウントのパスワードを指定します。 **/P**を省略した場合、 **gpresult**はパスワードの入力を求めます。 **/p**は **/x**または **/h**と共に使用することはできません。            |
| /user [\<TARGETDOMAIN @ no__t-1 @ no__t] \<TARGETUSER @ no__t |                                                                            RSoP データを表示するリモートユーザーを指定します。                                                                             |
|      /scope {ユーザー &#124;コンピューター}       |                                ユーザーまたはコンピューターの RSoP データを表示します。 **/Scope**を省略した場合、 **gpresult**はユーザーとコンピューターの両方の RSoP データを表示します。                                 |
|        [/x &#124; /h] <FILENAME>         | は、 *FILENAME*パラメーターで指定されたファイル名を使用して、レポートを XML ( **/x**) 形式または HTML 形式 ( **/h**) 形式で保存します。 **/U**、 **/p**、 **/r**、 **/v**、または **/z**と共に使用することはできません。 |
|                    /f                    |                                                           **/x**または **/h**オプションで指定されたファイル名を強制的に**gpresult**に上書きします。                                                           |
|                    /r                    |                                                                                             RSoP の概要データを表示します。                                                                                              |
|                    /v                    |                                                    詳細なポリシー情報を表示します。 これには、優先順位1で適用された詳細設定が含まれます。                                                    |
|                    /z                    |                                     グループポリシーに関する利用可能なすべての情報を表示します。 これには、1以上の優先順位で適用された詳細設定が含まれます。                                      |
|                    /?                    |                                                                                         コマンド プロンプトにヘルプを表示します。                                                                                         |

## <a name="remarks"></a>コメント
- グループポリシーは、組織内のユーザーとコンピューターに対してプログラム、ネットワークリソース、およびオペレーティングシステムがどのように動作するかを定義および制御するための主要な管理ツールです。 Active directory 環境では、グループポリシーは、サイト、ドメイン、または組織単位のメンバーシップに基づいてユーザーまたはコンピューターに適用されます。
- 重複したポリシー設定を任意のコンピューターまたはユーザーに適用できるため、グループポリシー機能によって、ユーザーがログオンしたときに生成されるポリシー設定のセットが生成されます。 **[gpresult]** を使用すると、ユーザーがログオンしたときに、指定したユーザーのコンピューターに適用されたポリシー設定の結果セットが表示されます。
- **/V**および **/z**では多くの情報が生成されるため、出力をテキストファイルにリダイレクトすると便利です (たとえば、 **gpresult/z > test.txt**)。
- **Gpresult**コマンドは、windows server 2012、windows Server 2008 R2、windows Server 2008、windows 8、windows 7、および windows Vista で使用できます。
  ## <a name="examples"></a>使用例
  次の例では、コンピューターの**srvmain**のリモートユーザー **targetusername**の rsop データを取得し、そのユーザーについてのみ rsop データを表示します。 このコマンドは、ユーザー **maindom\hiropln**の資格情報を使用して実行され、そのユーザーのパスワードとして<strong>p@ssW23</strong>が入力されます。

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /scope user /r
  ```
  
次の例では、 **targetusername**という名前のファイルに対して、コンピューター **srvmain**のリモートユーザーのグループポリシーに関する利用可能なすべての情報を保存**します。** コンピューターに関するデータは含まれていません。 このコマンドは、ユーザー **maindom\hiropln**の資格情報を使用して実行され、そのユーザーのパスワードとして<strong>p@ssW23</strong>が入力されます。

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /z > policy.txt
  ```
  
次の例では、コンピューターの**srvmain**とログオンユーザーの RSoP データを表示します。 データは、ユーザーとコンピューターの両方に含まれます。 このコマンドは、ユーザー **maindom\hiropln**の資格情報を使用して実行され、そのユーザーのパスワードとして<strong>p@ssW23</strong>が入力されます。

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /r
  ```
  
## <a name="additional-references"></a>その他の参照情報
- [グループポリシー TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)

- [コマンド ライン構文の記号](command-line-syntax-key.md)
