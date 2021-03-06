---
title: secedit
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58ed57ed-08e3-403d-a363-0620b358637a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c70211cc029cec7e6bb0290877089ecb9a86f22
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441463"
---
# <a name="secedit"></a>secedit



構成し、指定したセキュリティ テンプレートと現在の構成を比較することによってシステムのセキュリティを分析します。

## <a name="syntax"></a>構文

```
secedit 
[/analyze /db <database file name> /cfg <configuration file name> [/overwrite] /log <log file name> [/quiet]]
[/configure /db <database file name> [/cfg <configuration filename>] [/overwrite] [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]]
[/export /db <database file name> [/mergedpolicy] /cfg <configuration file name> [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>]]
[/generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback file name> [/log <log file name>] [/quiet]]
[/import /db <database file name> /cfg <configuration file name> [/overwrite] [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]]
[/validate <configuration file name>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[Secedit:analyze](secedit-analyze.md)|データベースに格納されているベースライン設定に対する現在のシステム設定を分析できます。  分析結果は、データベースの独立した領域には保存され、セキュリティの構成と分析スナップインで表示できます。|
|[Secedit:configure](secedit-configure.md)|使用すると、システム データベースに格納されているセキュリティ設定を構成できます。|
|[Secedit:export](secedit-export.md)|データベースに格納されているセキュリティ設定をエクスポートできます。|
|[Secedit:generaterollback](secedit-generaterollback.md)|構成テンプレートに関してロールバック テンプレートを生成できます。|
|[Secedit:import](secedit-import.md)|テンプレートで指定された設定をシステムに適用またはシステムに照らして分析できるように、データベースにセキュリティ テンプレートをインポートできます。|
|[Secedit:validate](secedit-validate.md)|セキュリティ テンプレートの構文を検証できます。|

## <a name="remarks"></a>注釈

すべてのファイル名のパスが指定されていない場合、現在のディレクトリが使用されます。

セキュリティ テンプレート スナップイン、およびセキュリティの構成を使用して、セキュリティ テンプレートが作成され、スナップインの分析が実行時に、次のファイルが作成されます。


|           ファイル           |                                                                                                                                                                                                                                                               説明                                                                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        Scesrv.log        |                                                                                                                             **場所**: %windir%\security\logs</br>**によって作成された**: オペレーティング システム</br>**ファイルの種類**: テキスト</br>**リフレッシュ レート**:ときに上書き secedit/分析、/構成/エクスポートまたは/import を実行します。</br>**[コンテンツ]** :ポリシーの種類でグループ化された分析の結果が含まれています。                                                                                                                             |
| *ユーザーが選択した名前*.sdb |                                                                                    **場所**: %windir%\*ユーザー アカウント<em>\Documents\Security\Database</br></em>*によって作成された*<em>: セキュリティの構成と分析スナップインで実行されています。</br></em>*ファイルの種類*<em>: 専用</br></em>*リフレッシュ レート*<em>:新しいセキュリティ テンプレートが作成されるたびに更新されます。</br></em>*コンテンツ*\*:ローカル セキュリティ ポリシーとユーザーが作成したセキュリティ テンプレート。                                                                                    |
| *ユーザーが選択した名前*.log | **場所**:ユーザー定義の既定値は %windir% が\*ユーザー アカウント<em>\Documents\Security\Logs</br></em>*によって作成された*<em>:実行している、/analyze と/サブコマンドを構成する (またはセキュリティの構成と分析スナップインを使用して)</br></em>*ファイルの種類*<em>: テキスト</br></em>*リフレッシュ レート*<em>:実行している、/analyze、/、サブコマンドを構成する (またはセキュリティの構成と分析スナップインを使用して)。上書きされます。</br></em>*コンテンツ*\*:</br>1. ログ ファイル名</br>2. Date and time (日付と時刻)</br>3.分析や調査の結果。 |
| *ユーザーが選択した名前*.inf |                                                                                     **場所**: %windir%\*ユーザー アカウント<em>\Documents\Security\Templates</br></em>*によって作成された*<em>: セキュリティ テンプレート スナップインを実行しています。</br></em>*ファイルの種類*<em>: テキスト</br></em>*リフレッシュ レート*<em>: セキュリティ テンプレートが更新されるたびに</br></em>*コンテンツ*\*:テンプレート、スナップインを使用して選択した各ポリシーに関する情報の設定が含まれています。                                                                                     |

> [!NOTE]
> Microsoft 管理コンソール (MMC) とセキュリティの構成と分析スナップインでは、Server Core では使用できません。

#### <a name="additional-references"></a>その他の参照情報

このコマンドの使用方法の例については、サブコマンドのファイルのいずれかの例を参照してください。
-   [コマンド ライン構文の記号](command-line-syntax-key.md)