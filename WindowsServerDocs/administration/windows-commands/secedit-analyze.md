---
title: 'secedit: 分析'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3430cf9d-1411-48b1-b5a9-2e47701dc87f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ae331b890d0e4201e8b621e5d84f5025934efa0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722095"
---
# <a name="seceditanalyze"></a>secedit: 分析



データベースに格納されているベースライン設定に対する現在のシステム設定を分析できます。

## <a name="syntax"></a>構文

```
Secedit /analyze /db <database file name> [/cfg <configuration file name>] [/overwrite] [/log <log file name>] [/quiet}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|db|必須。</br>分析を実行する、格納されている構成を含んでいるデータベースのパスとファイル名を指定します。</br>ファイル名をそれに関連付けられているセキュリティ テンプレート (ように、構成ファイルによって表される) されていないデータベースを指定する場合、 `/cfg \<configuration file name>` でもコマンド ライン オプションに指定する必要があります。|
|cfg|任意。</br>分析用のデータベースにインポートするセキュリティ テンプレートのパスとファイル名を指定します。</br>この/cfg オプションを使用すると、 `/db \<database file name>` パラメーター。 これが指定されていない場合、データベースに既に格納されている構成に対して分析を実行します。|
|overwrite|任意。</br>/Cfg パラメーターで、セキュリティ テンプレートがテンプレートまたは格納されているテンプレートに追加する代わりにデータベースに格納されている複合のテンプレートを上書きするかどうかを指定します。</br>このコマンド ライン オプションは有効な場合に、 `/cfg \<configuration file name>` パラメーターと共に使用します。 これが指定されていない場合、/cfg パラメーター内のテンプレートが格納されているテンプレートに追加されます。|
|log|任意。</br>プロセスで使用するログ ファイルのパスとファイル名を指定します。|
|quiet|任意。</br>画面出力を抑制します。 できます分析結果を表示する、セキュリティの構成と分析スナップインを Microsoft 管理コンソール (MMC) を使用しています。|

## <a name="remarks"></a>Remarks

分析結果は、データベースの独立した領域には保存され、セキュリティの構成と分析スナップインを MMC で表示できます。

ログ ファイルのパスを指定しない場合、既定のログ ファイル (*systemroot*\Documents and 設定\*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>.log) を使用します。

Windows Server 2008 で `Secedit /refreshpolicy` に置き換えられました `gpupdate`します。 セキュリティ設定を更新する方法については、次を参照してください。 [Gpupdate](gpupdate.md)します。

## <a name="examples"></a>例

セキュリティのデータベースにセキュリティの構成と分析スナップインを使用して作成した SecDbContoso.sdb のセキュリティのパラメーターの解析を実行します。 コマンドを確認できるようにメッセージが表示 SecAnalysisContosoFY11 が正しく実行されたファイルへの出力に指示します。
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
たとえば、分析によっていくつかの inadequacies が明らかになり、セキュリティテンプレート SecContoso .inf が変更されたとします。 コマンド プロンプトは表示されず、既存のファイル SecAnalysisContosoFY11 への出力、変更を反映するには、もう一度実行します。
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

## <a name="additional-references"></a>その他のリファレンス

-   [Secedit](secedit.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)