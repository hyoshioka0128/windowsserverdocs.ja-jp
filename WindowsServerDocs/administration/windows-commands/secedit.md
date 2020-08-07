---
title: secedit
description: 参照記事 * * * *-
ms.topic: article
ms.assetid: 58ed57ed-08e3-403d-a363-0620b358637a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 570590710ea10758fe35e1cc2160709885bb60eb
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882899"
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

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[Secedit:analyze](secedit-analyze.md)|データベースに格納されているベースライン設定に対する現在のシステム設定を分析できます。  分析結果は、データベースの独立した領域には保存され、セキュリティの構成と分析スナップインで表示できます。|
|[Secedit:configure](secedit-configure.md)|使用すると、システム データベースに格納されているセキュリティ設定を構成できます。|
|[Secedit:export](secedit-export.md)|データベースに格納されているセキュリティ設定をエクスポートできます。|
|[Secedit:generaterollback](secedit-generaterollback.md)|構成テンプレートに関してロールバック テンプレートを生成できます。|
|[Secedit:import](secedit-import.md)|テンプレートで指定された設定をシステムに適用またはシステムに照らして分析できるように、データベースにセキュリティ テンプレートをインポートできます。|
|[Secedit:validate](secedit-validate.md)|セキュリティ テンプレートの構文を検証できます。|

## <a name="remarks"></a>Remarks

すべてのファイル名のパスが指定されていない場合、現在のディレクトリが使用されます。

セキュリティ テンプレート スナップイン、およびセキュリティの構成を使用して、セキュリティ テンプレートが作成され、[スナップインの分析が実行時に、次のファイルが作成されます。


|           ファイル           |                                                                                                                                                                                                                                                               説明                                                                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        Scesrv.log        |                                                                                                                             **場所**: %windir%\security\logs</br>**によって作成された**: オペレーティング システム</br>**ファイルの種類**: テキスト</br>**リフレッシュ レート**: ときに上書き secedit、分析を構成する、エクスポートまたは/import を実行します。</br>**コンテンツ**: ポリシーの種類でグループ化された分析の結果が含まれています。                                                                                                                             |
| *ユーザーが選択した名前*.sdb |                                                                                    **場所**: %windir%\*ユーザー アカウント<em>\Documents\Security\Database</br></em>*作成者* <em> : セキュリティの構成と分析スナップインを実行する</br></em>*ファイルの種類* <em> : 専有</br></em>*更新頻度* <em> : 新しいセキュリティテンプレートが作成されるたびに更新されます。</br></em>*コンテンツ* \* : ローカルセキュリティポリシーとユーザーが作成したセキュリティテンプレート。                                                                                    |
| *ユーザーが選択した名前*.log | **場所**: ユーザー定義しますが、既定値は %windir%\*ユーザー アカウント<em>\Documents\Security\Logs</br></em>*作成者* <em> :/analyze および/configure サブコマンドを実行する (またはセキュリティの構成と分析スナップインを使用する)</br></em>*ファイルの種類* <em> : テキスト</br></em>*リフレッシュレート* <em> :/analyze および/configure サブコマンドを実行する (またはセキュリティの構成と分析スナップインを使用する)。上書きします。</br></em>*コンテンツ* \* :</br>1. ログファイル名</br>2. 日付と時刻</br>3. 分析または調査の結果。 |
| *ユーザーが選択した名前*.inf |                                                                                     **場所**: %windir%\*ユーザー アカウント<em>\Documents\Security\Templates</br></em>*作成者* <em> : セキュリティテンプレートスナップインの実行</br></em>*ファイルの種類* <em> : テキスト</br></em>*更新頻度* <em> : セキュリティテンプレートが更新されるたびに、</br></em>*コンテンツ* \* : スナップインを使用して選択した各ポリシーのテンプレートに関する設定情報が含まれます。                                                                                     |

> [!NOTE]
> Microsoft 管理コンソール (MMC) とセキュリティの構成と分析スナップインでは、Server Core では使用できません。

## <a name="additional-references"></a>その他の参照情報

このコマンドの使用方法の例については、サブコマンドのファイルのいずれかの例を参照してください。
- [コマンド ライン構文の記号](command-line-syntax-key.md)