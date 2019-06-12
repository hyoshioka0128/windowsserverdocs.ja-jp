---
title: gpresult
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c5d96e7e1fcaeadbbc6b67e1c816a8810fd0e3b6
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811186"
---
# <a name="gpresult"></a>gpresult

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート ユーザーとコンピューターのポリシーの結果セット (RSoP) 情報が表示されます。
RSoP は、ファイアウォール経由でリモート ターゲット コンピューターのレポートを使用するには、ポートで着信ネットワーク トラフィックを許可するファイアウォール規則があります。

## <a name="syntax"></a>構文

```
gpresult [/s <system> [/u <USERNAME> [/p [<PASSWOrd>]]]] [/user [<TARGETDOMAIN>\]<TARGETUSER>] [/scope {user | computer}] {/r | /v | /z | [/x | /h] <FILENAME> [/f] | /?}
```

## <a name="parameters"></a>パラメーター

> [!NOTE]
> 使用する場合を除き **/でしょうか**、いずれかの出力オプションを含める必要があります **/r**、 **/v**、 **/z**、 **/x**、または。 **/h**します。

|                パラメーター                 |                                                                                                     説明                                                                                                      |
|------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              /s\<システム\>               |                                                  名前またはリモート コンピューターの IP アドレスを指定します。 円記号を使用しないでください。 既定はローカル コンピュータです。                                                   |
|             /u\<ユーザー名\>              |                                コマンドを実行するのにには、指定したユーザーの資格情報を使用します。 既定のユーザーは、コマンドを発行しているコンピューターにログオンしているユーザーです。                                 |
|            /p [\<PASSWOrd\>]             |            提供されるユーザー アカウントのパスワードを指定します、 **/u**パラメーター。 場合 **/p**を省略すると、 **gpresult**パスワードの入力を要求します。 **/p**では使用できません **/x**または **/h**します。            |
| /user [\<TARGETDOMAIN\>\\]\<TARGETUSER\> |                                                                            RSoP データが表示される、リモート ユーザーを指定します。                                                                             |
|      /scope {user &#124; computer}       |                                ユーザーまたはコンピューターの RSoP データを表示します。 場合 **/スコープ**を省略すると、 **gpresult** RSoP データ、ユーザーとコンピューターの両方が表示されます。                                 |
|        [/x &#124; /h] <FILENAME>         | いずれかの XML でレポートを保存します ( **/x**) または HTML ( **/h**) 形式で指定されているファイル名と場所に、 *FILENAME*パラメーター。 は使用できません **/u**、 **/p**、 **/r**、 **/v**、または **/z**します。 |
|                    /f                    |                                                           強制的に**gpresult**で指定されているファイル名を上書きする、 **/x**または **/h**オプション。                                                           |
|                    /r                    |                                                                                             RSoP データの概要が表示されます。                                                                                              |
|                    /v                    |                                                    詳細なポリシー情報が表示されます。 これには、1 の優先順位で適用された詳細な設定が含まれます。                                                    |
|                    /z                    |                                     グループ ポリシーに関するすべての情報が表示されます。 これには、1 つ以上の優先順位で適用された詳細な設定が含まれます。                                      |
|                    /?                    |                                                                                         コマンド プロンプトにヘルプを表示します。                                                                                         |

## <a name="remarks"></a>注釈
- グループ ポリシーは、定義すると、組織内のユーザーとコンピューターのプログラム、ネットワーク リソース、およびオペレーティング システムの動作を制御する主要な管理ツールです。 Active directory 環境では、グループ ポリシーはユーザーまたはサイト、ドメイン、または組織単位のメンバーシップに基づいて、コンピューターに適用されます。
- 重複するポリシー設定を適用すると、ユーザーまたはコンピューターに、ために、グループ ポリシー機能は、ユーザーがログオンしたときに、結果として得られる一連のポリシー設定を生成します。 **gpresult**ユーザーがログオンしているときに指定したユーザーのコンピューターに適用されたポリシー設定の結果セットを表示します。
- **/V**と **/z**多くを生成、情報の出力をテキスト ファイルにリダイレクトすると便利です (たとえば、 **gpresult/z > policy.txt**)。
- **Gpresult**コマンドは Windows Server 2012、Windows Server 2008 R2、Windows server 2008、Windows 8、Windows 7、および Windows Vista で使用できます。
  ## <a name="examples"></a>例
  次の例は、リモート ユーザーの RSoP データを取得**targetusername**コンピューターの**srvmain**、のみのユーザーについての RSoP データを表示します。 ユーザーの資格情報でコマンドを実行**maindom\hiropln**、および<strong>p@ssW23</strong>そのユーザーのパスワードを入力します。

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /scope user /r
  ```
  
次の例は、リモート ユーザーのグループ ポリシーに関するすべての情報を保存**targetusername**コンピューターの**srvmain**という名前のファイルに**policy.txt**. データが、コンピューターの詳細については含まれません。 ユーザーの資格情報でコマンドを実行**maindom\hiropln**、および<strong>p@ssW23</strong>そのユーザーのパスワードを入力します。

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /z > policy.txt
  ```
  
次の例は、コンピューターの RSoP データを表示します。 **srvmain**とユーザーのログオンします。 データは、ユーザーとコンピューターの両方について含まれています。 ユーザーの資格情報でコマンドを実行**maindom\hiropln**、および<strong>p@ssW23</strong>そのユーザーのパスワードを入力します。

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /r
  ```
  
## <a name="additional-references"></a>その他の参照
- [グループ ポリシーの TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)

- [コマンド ライン構文の記号](command-line-syntax-key.md)
