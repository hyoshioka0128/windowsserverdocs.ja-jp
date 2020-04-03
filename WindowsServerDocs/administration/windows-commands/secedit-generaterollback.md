---
title: 'secedit: generaterollback'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 385a6799-51a7-4fe3-bd73-10c7998b6680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 797f93f010a903d6ec21f568d8d665cb2e42e692
ms.sourcegitcommit: 5ed817fff1262e390403a4f4f6c38fdc12300c29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75702743"
---
# <a name="seceditgeneraterollback"></a>secedit: generaterollback



指定した構成テンプレートのロールバック テンプレートを生成できます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
Secedit /generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback template file name> [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|db|必須。</br>分析を実行する、格納されている構成を含んでいるデータベースのパスとファイル名を指定します。</br>ファイル名をそれに関連付けられているセキュリティ テンプレート (ように、構成ファイルによって表される) されていないデータベースを指定する場合、 `/cfg \<configuration file name>` でもコマンド ライン オプションに指定する必要があります。|
|cfg|必須。</br>分析用のデータベースにインポートするセキュリティ テンプレートのパスとファイル名を指定します。</br>この/cfg オプションを使用すると、 `/db \<database file name>` パラメーター。 これが指定されていない場合、データベースに既に格納されている構成に対して分析を実行します。|
|rbk|必須。</br>ロールバック情報が書き込まれるセキュリティ テンプレートを指定します。 セキュリティ テンプレートを作成するには、セキュリティ テンプレート スナップインを使用します。 次のコマンドでは、ロールバック ファイルを作成できます。|
|ログ|(省略可能)。</br>プロセスのログ ファイルのパスとファイル名を指定します。|
|通知の停止|(省略可能)。</br>画面とログの出力を抑制します。 できます分析結果を表示する、セキュリティの構成と分析スナップインを Microsoft 管理コンソール (MMC) を使用しています。|

## <a name="remarks"></a>注釈

ログ ファイルのパスを指定しない場合、既定のログ ファイル (*systemroot*\Users \*<em>UserAccount\*\My Documents\Security\Logs</em>DatabaseName.log) を使用します。

Windows Server 2008 で始まる `Secedit /refreshpolicy` に置き換えられました `gpupdate`します。 セキュリティ設定を更新する方法については、次を参照してください。 [Gpupdate](gpupdate.md)します。

このコマンドが正常に実行されると、"タスクが正常に完了しました。" という状態が表示されます。 指定されたセキュリティ テンプレートとセキュリティ ポリシーの構成間の不一致のみのログ。 Scesrv.log、これらの不一致が一覧表示します。

既存のロールバック テンプレートが指定されている場合、このコマンドが上書きされます。 次のコマンドでは、新しいロールバック テンプレートを作成できます。 どちらの条件は、追加のパラメーターは必要ありません。

## <a name="examples"></a><a name="BKMK_Examples"></a>例

セキュリティの構成と分析スナップインで、SecTmplContoso.inf を使用してセキュリティ テンプレートを作成した後、元の設定を保存するロールバック構成ファイルを作成します。 FY11 ログ ファイルにアクションを記述します。
```
Secedit /generaterollback /db C:\Security\FY11\SecDbContoso.sdb /cfg sectmplcontoso.inf /rbk sectmplcontosoRBK.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

#### <a name="additional-references"></a>その他の参照情報

-   [Secedit](secedit.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)