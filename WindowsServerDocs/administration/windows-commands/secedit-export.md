---
title: 'secedit: エクスポート'
description: 参照記事 * * * *-
ms.topic: article
ms.assetid: 49a8b241-aa8c-45b7-844d-67a29fab708e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5079ecc2874c1d834fb351ebb51bf140309e4248
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882983"
---
# <a name="seceditexport"></a>secedit: エクスポート



セキュリティ テンプレートで構成されるデータベースに格納されているセキュリティ設定をエクスポートします。

## <a name="syntax"></a>構文

```
Secedit /export /db <database file name> [/mergedpolicy] /cfg <configuration file name> [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|db|必須。</br>分析を実行する、格納されている構成を含んでいるデータベースのパスとファイル名を指定します。</br>ファイル名をそれに関連付けられているセキュリティ テンプレート (ように、構成ファイルによって表される) されていないデータベースを指定する場合、 `/cfg \<configuration file name>` でもコマンド ライン オプションに指定する必要があります。|
|mergedpolicy|省略可能。</br>マージし、ドメインとローカル ポリシーのセキュリティ設定をエクスポートします。|
|cfg|必須。</br>分析用のデータベースにインポートするセキュリティ テンプレートのパスとファイル名を指定します。</br>この/cfg オプションを使用すると、 `/db \<database file name>` パラメーター。 これが指定されていない場合、データベースに既に格納されている構成に対して分析を実行します。|
|領域|省略可能。</br>システムに適用するセキュリティ領域を指定します。 このパラメーターが指定されていない場合は、データベースで定義されているすべてのセキュリティ設定が、システムに適用されます。 複数の領域を構成するには、各領域をスペースで区切ります。 次のセキュリティの領域がサポートされています。</br>-SecurityPolicy</br>    ローカル ポリシーおよびアカウント ポリシーを含む、システムのドメイン ポリシーは、ポリシーやセキュリティ オプションを監査します。</br>-Group_Mgmt</br>    セキュリティ テンプレートで指定されたすべてのグループのグループの設定が制限されています。</br>-User_Rights</br>    ユーザーのログオン権限と特権の付与します。</br>-レジストリ</br>    ローカル レジストリ キーのセキュリティ。</br>-FileStore</br>    ローカル ファイル ストレージでのセキュリティ。</br>-サービス</br>    定義されているすべてのサービスのセキュリティ。|
|log|省略可能。</br>プロセスのログ ファイルのパスとファイル名を指定します。|
|quiet|省略可能。</br>画面とログの出力を抑制します。 できます分析結果を表示する、セキュリティの構成と分析スナップインを Microsoft 管理コンソール (MMC) を使用しています。|

## <a name="remarks"></a>Remarks

このコマンドを使用して、別のコンピューターに、設定をインポートするだけでなく、ローカル コンピューターで、セキュリティ ポリシーをバックアップできます。

ログ ファイルのパスを指定しない場合、既定のログ ファイル (*systemroot*\Documents and 設定\*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>.log) を使用します。

Windows Server 2008 で `Secedit /refreshpolicy` に置き換えられました `gpupdate`します。 セキュリティ設定を更新する方法については、次を参照してください。 [Gpupdate](gpupdate.md)します。

## <a name="examples"></a>例

セキュリティのデータベースと、ドメイン セキュリティ ポリシーを inf ファイルにエクスポートし、別のデータベースに別のコンピューターでセキュリティ ポリシー設定をレプリケートするためにそのファイルをインポートします。
```
Secedit /export /db C:\Security\FY11\SecDbContoso.sdb /mergedpolicy /cfg SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log /quiet
```
別のコンピューター上の別のデータベースにそのファイルをインポートします。
```
Secedit /import /db C:\Security\FY12\SecDbContoso.sdb /cfg SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY12.log /quiet
```

## <a name="additional-references"></a>その他の参照情報

-   [Secedit:import](secedit-import.md)
-   [Secedit](secedit.md)
- [コマンド ライン構文の記号](command-line-syntax-key.md)