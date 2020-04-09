---
title: 'secedit: 分析'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3430cf9d-1411-48b1-b5a9-2e47701dc87f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dca476237af48ef4222a47aefb8291571a5d66eb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835015"
---
# <a name="seceditanalyze"></a>secedit: 分析



データベースに格納されているベースライン設定に対する現在のシステム設定を分析できます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
Secedit /analyze /db <database file name> [/cfg <configuration file name>] [/overwrite] [/log <log file name>] [/quiet}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|db|必須。</br>分析を実行する、格納されている構成を含んでいるデータベースのパスとファイル名を指定します。</br>ファイル名をそれに関連付けられているセキュリティ テンプレート (ように、構成ファイルによって表される) されていないデータベースを指定する場合、 `/cfg \<configuration file name>` でもコマンド ライン オプションに指定する必要があります。|
|cfg|省略可。</br>分析用のデータベースにインポートするセキュリティ テンプレートのパスとファイル名を指定します。</br>この/cfg オプションを使用すると、 `/db \<database file name>` パラメーター。 これが指定されていない場合、データベースに既に格納されている構成に対して分析を実行します。|
|overwrite|省略可。</br>/Cfg パラメーターで、セキュリティ テンプレートがテンプレートまたは格納されているテンプレートに追加する代わりにデータベースに格納されている複合のテンプレートを上書きするかどうかを指定します。</br>このコマンド ライン オプションは有効な場合に、 `/cfg \<configuration file name>` パラメーターと共に使用します。 これが指定されていない場合、/cfg パラメーター内のテンプレートが格納されているテンプレートに追加されます。|
|log|省略可。</br>プロセスで使用するログ ファイルのパスとファイル名を指定します。|
|通知の停止|省略可。</br>画面出力を抑制します。 できます分析結果を表示する、セキュリティの構成と分析スナップインを Microsoft 管理コンソール (MMC) を使用しています。|

## <a name="remarks"></a>コメント

分析結果は、データベースの独立した領域には保存され、セキュリティの構成と分析スナップインを MMC で表示できます。

ログファイルのパスが指定されていない場合は、既定のログファイル (*systemroot*\Documents および Settings\*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>.log) が使用されます。

Windows Server 2008 で `Secedit /refreshpolicy` に置き換えられました `gpupdate`します。 セキュリティ設定を更新する方法については、次を参照してください。 [Gpupdate](gpupdate.md)します。

## <a name="examples"></a><a name=BKMK_Examples></a>例

セキュリティのデータベースにセキュリティの構成と分析スナップインを使用して作成した SecDbContoso.sdb のセキュリティのパラメーターの解析を実行します。 コマンドを確認できるようにメッセージが表示 SecAnalysisContosoFY11 が正しく実行されたファイルへの出力に指示します。
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
たとえば、分析によっていくつかの inadequacies が明らかになり、セキュリティテンプレート SecContoso .inf が変更されたとします。 コマンド プロンプトは表示されず、既存のファイル SecAnalysisContosoFY11 への出力、変更を反映するには、もう一度実行します。
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

## <a name="additional-references"></a>その他の参照情報

-   [Secedit](secedit.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)