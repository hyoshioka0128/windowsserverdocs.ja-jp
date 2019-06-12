---
title: 別のサーバー上のインポートには、NPS の構成をエクスポートします。
description: このトピックを使用すると、Windows Server 2016 でネットワーク ポリシー サーバーの構成をエクスポートするのに方法について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d268dc57-78f8-47ba-9a7a-a607e8b9225c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b95e39af63e284d0147335faabfb740c0dd175bc
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812294"
---
# <a name="export-an-nps-configuration-for-import-on-another-server"></a>別のサーバー上のインポートには、NPS の構成をエクスポートします。

適用先:Windows Server 2016

全体の NPS 構成をエクスポートすることができます-RADIUS クライアントとサーバー、ネットワーク ポリシー、接続要求ポリシー、レジストリ、およびログの構成を含む、別の NPS のインポート用の 1 つの NPS から。 

NPS 構成をエクスポートするのにには、次のツールのいずれかを使用します。

- Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 の場合は、Netsh を使用するまたは Windows PowerShell を使用することができます。
- Windows Server 2008 R2 および Windows Server 2008 では、Netsh を使用します。

> [!IMPORTANT]
> 元の NPS データベースに移行先 NPS データベースのバージョン番号より新しいバージョン番号がある場合は、この手順を使用しないでください。 表示から NPS データベースのバージョン番号を表示することができます、 **netsh nps 構成を表示する**コマンド。

ネットワーク経由で送信するエクスポートの XML ファイルでは、NPS の構成が暗号化されていないためがセキュリティが侵害、移行先サーバーへの移行元サーバーから XML ファイルを移動する場合の予防措置をかけて可能性があります。 たとえば、ファイルを移動する前に、暗号化されたパスワード保護されたアーカイブ ファイルにファイルを追加します。 さらに、悪意のあるユーザーがアクセスできないようにする安全な場所にファイルを格納します。

> [!NOTE]
> ソース NPS に SQL サーバーのログ記録を構成する場合、SQL Server のログ記録の設定は、XML ファイルにエクスポートされません。 別の NPS 上のファイルをインポートした後は、SQL Server のログを手動で構成する必要があります。

## <a name="export-and-import-the-nps-configuration-by-using-windows-powershell"></a>エクスポートし、Windows PowerShell を使用して NPS 構成をインポートします。

Windows Server 2012 およびそれ以降のオペレーティング システム バージョンでは、Windows PowerShell を使用して NPS 構成をエクスポートできます。

NPS 構成をエクスポートするためのコマンド構文は次のとおりです。 

    Export-NpsConfiguration -Path <filename>

次の表に、パラメーターを**エクスポート NpsConfiguration**で Windows PowerShell コマンドレット。 太字のパラメーターが必要です。

|パラメーター|説明|
|---------|-----------|
|パス|NPS の構成をエクスポートする XML ファイルの場所と名前を指定します。|

**管理者の資格情報**

この手順を完了するには、Administrators グループのメンバーがあります。

### <a name="export-example"></a>エクスポートの例 

次の例では、NPS の構成はローカル ドライブ上にある XML ファイルにエクスポートされます。 このコマンドを実行するには、ソース NPS で、Windows PowerShell を管理者として実行、次のコマンドを入力し、Enter キーを押します。

`Export-NpsConfiguration –Path c:\config.xml` 

詳細については、次を参照してください。[エクスポート NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx)します。

NPS 構成をエクスポートした後は、移行先サーバーに XML ファイルをコピーします。

移行先サーバーで NPS 構成をインポートするためのコマンド構文は次のとおりです。

    Import-NpsConfiguration [-Path] <String> [ <CommonParameters>]

### <a name="import-example"></a>インポートの例

次のコマンドは、NPS に C:\Npsconfig.xml という名前のファイルから設定をインポートします。 このコマンドを実行するには、移行先 NPS で、Windows PowerShell を管理者として実行、次のコマンドを入力および Enter キーを押します。

    PS C:\> Import-NpsConfiguration -Path "C:\Npsconfig.xml"

詳細については、次を参照してください。[インポート NpsConfiguration](https://technet.microsoft.com/library/jj872750.aspx)します。

## <a name="export-and-import-the-nps-configuration-by-using-netsh"></a>エクスポートおよび Netsh を使用して NPS 構成をインポートします。

ネットワーク シェルを使用する\(Netsh\)を使用して NPS の構成をエクスポートする、 **netsh nps エクスポート**コマンド。

ときに、 **netsh nps インポート**コマンドを実行すると、NPS は自動的に更新された構成設定を更新します。 NPS を実行する対象のコンピューターで停止する必要はありません、 **netsh nps インポート**コマンド、ただし、NPS コンソールまたは NPS MMC スナップインでは、構成のインポート中には開くが場合、サーバーの構成の変更は表示されませんまで表示を更新するとします。 

> [!NOTE]
> 使用すると、 **netsh nps エクスポート**コマンド、コマンド パラメーターを指定する必要が**exportPSK**値を持つ**はい**します。 このパラメーターと値を明示的に NPS の構成をエクスポートして、エクスポートされた XML ファイルが含まれている、RADIUS クライアントおよびリモート RADIUS サーバー グループのメンバーの共有シークレットが暗号化されていないことを理解することを記述します。

**管理者の資格情報**

この手順を完了するには、Administrators グループのメンバーがあります。

### <a name="to-copy-an-nps-configuration-to-another-nps-using-netsh-commands"></a>別の NPS の Netsh コマンドを使用するのには、NPS の構成をコピーするには

1. NPS のソースで開く**コマンド プロンプト**、型**netsh**、し、Enter キーを押します。

2. **Netsh**プロンプトで「 **nps**、し、Enter キーを押します。 

3. **Netsh nps**プロンプトで「**ファイル名のエクスポート =** "*path\file.xml*" **exportPSK = [はい]** ここで、 *のパス*は、NPS の構成ファイルを保存するフォルダーの場所と*ファイル*を保存する XML ファイルの名前を指定します。 Enter キーを押します。 

構成設定を保存\(レジストリ設定を含む\)XML ファイルにします。 相対または絶対パスを指定できますか、汎用名前付け規則であることができます\(UNC\)パス。 Enter を押すと、ファイルへのエクスポートが成功したかどうかを示すメッセージが表示されます。

4. NPS の移行先に作成したファイルをコピーします。

5. 移行先 NPS のコマンド プロンプトで「 **netsh nps インポート filename =** "*path\file.xml*"し、Enter キーを押します。 XML ファイルからインポートが成功したかどうかを示すメッセージが表示されます。

Netsh の詳細については、次を参照してください。[ネットワーク シェル (Netsh)](../netsh/netsh.md)します。

