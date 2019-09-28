---
title: 別のサーバーにインポートするために NPS 構成をエクスポートする
description: このトピックでは、Windows Server 2016 でネットワークポリシーサーバーの構成をエクスポートする方法について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d268dc57-78f8-47ba-9a7a-a607e8b9225c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cbebd0388ccd5dd2540a20f5d325d7f97c7e2bb3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405439"
---
# <a name="export-an-nps-configuration-for-import-on-another-server"></a>別のサーバーにインポートするために NPS 構成をエクスポートする

適用先:Windows Server 2016

Nps 構成全体 (RADIUS クライアントとサーバー、ネットワークポリシー、接続要求ポリシー、レジストリ、ログ構成など) を、別の nps にインポートするために1つの NPS からエクスポートできます。 

次のツールのいずれかを使用して、NPS の構成をエクスポートします。

- Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 では、Netsh を使用することも、Windows PowerShell を使用することもできます。
- Windows Server 2008 R2 および Windows Server 2008 では、Netsh を使用します。

> [!IMPORTANT]
> 移行元の NPS データベースのバージョン番号が、移行先の NPS データベースのバージョン番号よりも大きい場合は、この手順を使用しないでください。 NPS データベースのバージョン番号は、 **netsh nps show config**コマンドの表示から確認できます。

NPS の構成はエクスポートされた XML ファイルで暗号化されないため、ネットワーク経由で送信すると、セキュリティ上のリスクが生じる可能性があるため、移行元サーバーから移行先サーバーに XML ファイルを移動する際には注意が必要です。 たとえば、ファイルを移動する前に、暗号化されたパスワードで保護されたアーカイブファイルにファイルを追加します。 また、悪意のあるユーザーがアクセスできないように、ファイルを安全な場所に保存します。

> [!NOTE]
> ソース NPS で SQL Server ログ記録が構成されている場合、SQL Server ログ設定は XML ファイルにエクスポートされません。 別の NPS にファイルをインポートした後、SQL Server ログを手動で構成する必要があります。

## <a name="export-and-import-the-nps-configuration-by-using-windows-powershell"></a>Windows PowerShell を使用して NPS 構成をエクスポートおよびインポートする

Windows Server 2012 以降のバージョンのオペレーティングシステムでは、Windows PowerShell を使用して NPS の構成をエクスポートできます。

NPS 構成をエクスポートするためのコマンド構文は次のとおりです。 

    Export-NpsConfiguration -Path <filename>

次の表に、Windows PowerShell の**Export-NpsConfiguration**コマンドレットのパラメーターの一覧を示します。 太字のパラメーターが必要です。

|パラメーター|説明|
|---------|-----------|
|パス|NPS 構成をエクスポートする XML ファイルの名前と場所を指定します。|

**管理者の資格情報**

この手順を完了するには、Administrators グループのメンバーである必要があります。

### <a name="export-example"></a>エクスポートの例 

次の例では、NPS 構成がローカルドライブにある XML ファイルにエクスポートされます。 このコマンドを実行するには、移行元の NPS で管理者として Windows PowerShell を実行し、次のコマンドを入力して、Enter キーを押します。

`Export-NpsConfiguration –Path c:\config.xml` 

詳細については、「 [Export-NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx)」を参照してください。

NPS の構成をエクスポートした後、XML ファイルを移行先サーバーにコピーします。

移行先サーバーに NPS 構成をインポートするためのコマンド構文は次のとおりです。

    Import-NpsConfiguration [-Path] <String> [ <CommonParameters>]

### <a name="import-example"></a>インポートの例

次のコマンドは、C:\Npsconfig.xml という名前のファイルから NPS に設定をインポートします。 このコマンドを実行するには、移行先 NPS で管理者として Windows PowerShell を実行し、次のコマンドを入力して、Enter キーを押します。

    PS C:\> Import-NpsConfiguration -Path "C:\Npsconfig.xml"

詳細については、「 [Import-NpsConfiguration](https://technet.microsoft.com/library/jj872750.aspx)」を参照してください。

## <a name="export-and-import-the-nps-configuration-by-using-netsh"></a>Netsh を使用して NPS 構成をエクスポートおよびインポートする

**Netsh nps export**コマンドを使用して nps 構成をエクスポートするには、ネットワークシェル \(netsh @ no__t-1 を使用します。

**Netsh nps import**コマンドを実行すると、更新された構成設定を使用して nps が自動的に更新されます。 **Netsh nps import**コマンドを実行するために、セットアップ先のコンピューターで nps を停止する必要はありませんが、構成のインポート中に nps コンソールまたは nps MMC スナップインを開いている場合は、ビューを更新するまでサーバー構成への変更は表示されません。 

> [!NOTE]
> **Netsh nps export**コマンドを使用する場合は、 **[はい]** の値を使用してコマンドパラメーター **exportpsk**を指定する必要があります。 このパラメーターと値は、NPS 構成をエクスポートすること、および RADIUS クライアントとリモート RADIUS サーバーグループのメンバーについて、エクスポートされた XML ファイルに暗号化されていない共有シークレットが含まれていることを理解していることを明示的に示します。

**管理者の資格情報**

この手順を完了するには、Administrators グループのメンバーである必要があります。

### <a name="to-copy-an-nps-configuration-to-another-nps-using-netsh-commands"></a>Netsh コマンドを使用して NPS 構成を別の NPS にコピーするには

1. 移行元の NPS で、**コマンドプロンプト**を開き、「 **netsh**」と入力して、enter キーを押します。

2. **Netsh**プロンプトで、「 **nps**」と入力し、enter キーを押します。 

3. **Netsh nps**プロンプトで、「 **export filename =** "*PATH\FILE.XML*" **exportpsk = YES**」と入力します。ここで、 *path*は nps 構成ファイルを保存するフォルダーの場所であり、 *file*は xml ファイルの名前です。を保存します。 Enter キーを押します。 

これには、レジストリ設定 @ no__t などの構成 @no__t 設定が XML ファイルに格納されます。 相対パスまたは絶対パスを指定することも、汎用名前付け @no__t 規則 (0 UNC @ no__t のパス) を指定することもできます。 Enter キーを押すと、ファイルへのエクスポートが正常に完了したかどうかを示すメッセージが表示されます。

4. 作成したファイルを移行先 NPS にコピーします。

5. 移行先 NPS のコマンドプロンプトで、「 **netsh nps import filename =** "*path\file.xml*"」と入力し、enter キーを押します。 XML ファイルからのインポートが正常に完了したかどうかを示すメッセージが表示されます。

Netsh の詳細については、「[ネットワークシェル (netsh)](../netsh/netsh.md)」を参照してください。

