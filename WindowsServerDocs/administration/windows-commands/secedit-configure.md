---
title: 'secedit: 構成'
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a92e68ca-003c-4219-8655-0e7734f5fab3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8285c22c3c64b4f056124d8a1bb02297c7aea3c8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853393"
---
# <a name="seceditconfigure"></a>secedit: 構成



データベースに格納されているセキュリティ設定を使用して現在のシステム設定を構成できます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
Secedit /configure /db <database file name> [/cfg <configuration file name>] [/overwrite] [/areas SECURITYPOLICY | GROUP_MGMT | USER_RIGHTS | REGKEYS | FILESTORE | SERVICES] [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|db|必須。</br>格納されている構成を含んでいるデータベースのパスとファイル名を指定します。</br>ファイル名をそれに関連付けられているセキュリティ テンプレート (ように、構成ファイルによって表される) されていないデータベースを指定する場合、 `/cfg \<configuration file name>` でもコマンド ライン オプションに指定する必要があります。|
|cfg|任意。</br>分析用のデータベースにインポートするセキュリティ テンプレートのパスとファイル名を指定します。</br>この/cfg オプションを使用すると、 `/db \<database file name>` パラメーター。 これが指定されていない場合、データベースに既に格納されている構成に対して分析を実行します。|
|overwrite|(省略可能)。</br>/Cfg パラメーターで、セキュリティ テンプレートがテンプレートまたは格納されているテンプレートに追加する代わりにデータベースに格納されている複合のテンプレートを上書きするかどうかを指定します。</br>このコマンド ライン オプションは有効な場合に、 `/cfg \<configuration file name>` パラメーターと共に使用します。 これが指定されていない場合、/cfg パラメーター内のテンプレートが格納されているテンプレートに追加されます。|
|領域|(省略可能)。</br>システムに適用するセキュリティ領域を指定します。 このパラメーターが指定されていない場合は、データベースで定義されているすべてのセキュリティ設定が、システムに適用されます。 複数の領域を構成するには、各領域をスペースで区切ります。 次のセキュリティの領域がサポートされています。</br>-SecurityPolicy</br>    ローカル ポリシーおよびアカウント ポリシーを含む、システムのドメイン ポリシーは、ポリシーやセキュリティ オプションを監査します。</br>-Group_Mgmt</br>    セキュリティ テンプレートで指定されたすべてのグループのグループの設定が制限されています。</br>-User_Rights</br>    ユーザーのログオン権限と特権の付与します。</br>-レジストリ</br>    ローカル レジストリ キーのセキュリティ。</br>-FileStore</br>    ローカル ファイル ストレージでのセキュリティ。</br>-サービス</br>    定義されているすべてのサービスのセキュリティ。|
|ログ|任意。</br>プロセスのログ ファイルのパスとファイル名を指定します。|
|通知の停止|(省略可能)。</br>画面とログの出力を抑制します。 できます分析結果を表示する、セキュリティの構成と分析スナップインを Microsoft 管理コンソール (MMC) を使用しています。|

## <a name="remarks"></a>注釈

ログ ファイルのパス指定しない場合は、既定のログ ファイル (*systemroot*\Users \*& #93;*\My Documents\Security\Logs\*DatabaseName*.log) が使用されます。

Windows Server 2008 で始まる `Secedit /refreshpolicy` に置き換えられました `gpupdate`します。 セキュリティ設定を更新する方法については、次を参照してください。 [Gpupdate](gpupdate.md)します。

## <a name="BKMK_Examples"></a>例

セキュリティのデータベースにセキュリティの構成と分析スナップインを使用して作成した SecDbContoso.sdb のセキュリティのパラメーターの解析を実行します。 コマンドを確認できるようにメッセージが表示 SecAnalysisContosoFY11 が正しく実行されたファイルへの出力に指示します。
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
たとえば、ある、分析によるといくつかの不備および SecContoso.inf、セキュリティ テンプレートが変更されたためにとします。 コマンド プロンプトは表示されず、既存のファイル SecAnalysisContosoFY11 への出力、変更を反映するには、もう一度実行します。
```
Secedit /configure /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

#### <a name="additional-references"></a>その他の参照情報

-   [Secedit](secedit.md)
-   [secedit: 分析](secedit-analyze.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)