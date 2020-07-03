---
title: 'secedit: generaterollback'
description: 参照記事 * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 385a6799-51a7-4fe3-bd73-10c7998b6680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1dec7833853d3c0526997f1d3e1bd2113d114cf2
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926175"
---
# <a name="seceditgeneraterollback"></a>secedit: generaterollback



指定した構成テンプレートのロールバック テンプレートを生成できます。

## <a name="syntax"></a>構文

```
Secedit /generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback template file name> [/log <log file name>] [/quiet]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|db|必須です。</br>分析を実行する、格納されている構成を含んでいるデータベースのパスとファイル名を指定します。</br>ファイル名をそれに関連付けられているセキュリティ テンプレート (ように、構成ファイルによって表される) されていないデータベースを指定する場合、 `/cfg \<configuration file name>` でもコマンド ライン オプションに指定する必要があります。|
|cfg|必須です。</br>分析用のデータベースにインポートするセキュリティ テンプレートのパスとファイル名を指定します。</br>この/cfg オプションを使用すると、 `/db \<database file name>` パラメーター。 これが指定されていない場合、データベースに既に格納されている構成に対して分析を実行します。|
|rbk|必須です。</br>ロールバック情報が書き込まれるセキュリティ テンプレートを指定します。 セキュリティ テンプレートを作成するには、セキュリティ テンプレート スナップインを使用します。 次のコマンドでは、ロールバック ファイルを作成できます。|
|log|任意。</br>プロセスのログ ファイルのパスとファイル名を指定します。|
|quiet|任意。</br>画面とログの出力を抑制します。 できます分析結果を表示する、セキュリティの構成と分析スナップインを Microsoft 管理コンソール (MMC) を使用しています。|

## <a name="remarks"></a>注釈

ログ ファイルのパスを指定しない場合、既定のログ ファイル (*systemroot*\Users \*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>.log) を使用します。

Windows Server 2008 で始まる `Secedit /refreshpolicy` に置き換えられました `gpupdate`します。 セキュリティ設定を更新する方法については、次を参照してください。 [Gpupdate](gpupdate.md)します。

このコマンドが正常に実行されると、タスクが正常に完了したことが表示されます。 指定されたセキュリティ テンプレートとセキュリティ ポリシーの構成間の不一致のみのログ。 Scesrv.log、これらの不一致が一覧表示します。

既存のロールバック テンプレートが指定されている場合、このコマンドが上書きされます。 次のコマンドでは、新しいロールバック テンプレートを作成できます。 どちらの条件は、追加のパラメーターは必要ありません。

## <a name="examples"></a>例

セキュリティの構成と分析スナップインで、SecTmplContoso.inf を使用してセキュリティ テンプレートを作成した後、元の設定を保存するロールバック構成ファイルを作成します。 FY11 ログ ファイルにアクションを記述します。
```
Secedit /generaterollback /db C:\Security\FY11\SecDbContoso.sdb /cfg sectmplcontoso.inf /rbk sectmplcontosoRBK.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

## <a name="additional-references"></a>その他の参照情報

-   [Secedit](secedit.md)
- [コマンド ライン構文の記号](command-line-syntax-key.md)