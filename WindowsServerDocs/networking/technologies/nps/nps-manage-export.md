---
title: NPS サーバーの構成を別のサーバーにインポートのエクスポートします。
description: このトピックを使用すると、Windows Server 2016 でネットワーク ポリシー サーバーの構成をエクスポートするのに方法について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d268dc57-78f8-47ba-9a7a-a607e8b9225c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 141a99e930672d8403315cb6804290d184ef3007
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="export-an-nps-server-configuration-for-import-on-another-server"></a>NPS サーバーの構成を別のサーバーにインポートのエクスポートします。

Windows Server 2016 の適用対象:

全体の NPS の構成をエクスポートする — RADIUS クライアントとサーバー、ネットワーク ポリシー、接続要求ポリシー、レジストリ、およびログの構成を含む — から別の NPS サーバーの別の NPS サーバーにインポートします。 

NPS の構成をエクスポートするのにには、ツールは、次のいずれかを使用します。

- Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 では、Netsh を使用することができますか Windows PowerShell を使用することができます。
- Windows Server 2008 R2 および Windows Server 2008 では、Netsh を使用します。

>[!IMPORTANT]
>移行元 NPS データベース、移行先 NPS データベースのバージョン番号よりも高いバージョン番号がある場合、この手順を使用しません。 NPS の表示からデータベースのバージョン番号を表示することができます、**netsh nps の構成を表示する**コマンド。

NPS サーバーの構成暗号化されないため、エクスポートされた XML ファイルで、セキュリティ上のリスクを引き起こす可能性がそれをネットワーク経由で送信するので予防 XML ファイルを移行元サーバーから移行先サーバーに移動する場合。 たとえば、ファイルを移動する前に、暗号化されたパスワード保護されているアーカイブ ファイルにファイルを追加します。 さらに、悪意のあるユーザーがアクセスできないようにする安全な場所にファイルを保存します。

>[!NOTE]
>SQL Server のログが移行元 NPS サーバーで構成されている場合、SQL Server のログ記録の設定は XML ファイルにエクスポートされません。 別の NPS サーバー上のファイルをインポートした後は、SQL Server のログを手動で構成する必要があります。

## <a name="export-and-import-the-nps-configuration-by-using-windows-powershell"></a>エクスポートし、Windows PowerShell を使用して、NPS の構成をインポートします。

Windows Server 2012 およびそれ以降のオペレーティング システム バージョンでは、Windows PowerShell を使用して、NPS の構成をエクスポートすることができます。

NPS の構成をエクスポートするためのコマンド構文は次のとおりです。 

    Export-NpsConfiguration -Path <filename>

次の表に、パラメーター、**エクスポート NpsConfiguration** Windows PowerShell のコマンドレットです。 太字でパラメーターが必要です。

|パラメーター|説明|
|---------|-----------|
|パス|NPS サーバーの構成をエクスポートする XML ファイルの場所と名前を指定します。|

**管理者の資格情報**

この手順を完了するには、Administrators グループのメンバーがあります。

### <a name="export-example"></a>エクスポートの例 

次の例では、NPS の構成はローカル ドライブ上にある XML ファイルにエクスポートされます。 このコマンドを実行するには、移行元 NPS サーバーで Windows PowerShell を管理者として実行、次のコマンドを入力および Enter キーを押します。

`Export-NpsConfiguration –Path c:\config.xml` 

詳細については、次を参照してください。[エクスポート NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx)します。

NPS の構成をエクスポートした後は、移行先サーバーに XML ファイルをコピーします。

移行先サーバーに NPS の構成をインポートするためのコマンド構文は次のとおりです。

    Import-NpsConfiguration [-Path] <String> [ <CommonParameters>]

### <a name="import-example"></a>インポートの例

次のコマンドは、NPS を C:\Npsconfig.xml をという名前のファイルから設定をインポートします。 このコマンドを実行するには、移行先 NPS サーバーで Windows PowerShell を管理者として実行、次のコマンドを入力および Enter キーを押します。

    PS C:\> Import-NpsConfiguration -Path "C:\Npsconfig.xml"

詳細については、次を参照してください。[インポート NpsConfiguration](https://technet.microsoft.com/library/jj872750.aspx)します。

## <a name="export-and-import-the-nps-configuration-by-using-netsh"></a>エクスポートし、Netsh を使用した NPS の構成をインポート

ネットワーク シェル \(Netsh\) を使用するを使用して、NPS サーバーの構成をエクスポート、**netsh nps エクスポート**コマンド。

ときに、**netsh nps インポート**コマンドの実行、NPS が更新された構成設定を使って自動的に更新します。 NPS を実行する移行先コンピューターを停止する必要はありません、**netsh nps インポート**コマンド、ただし NPS コンソールまたは NPS MMC スナップインで開いて場合は、構成のインポート中に、サーバー構成の変更までは表示されません表示を更新します。 

>[!NOTE]
>使用すると、**netsh nps エクスポート**コマンドをコマンドのパラメーターを指定する必要が**exportPSK**値を持つ**はい**します。 このパラメーターと値を明示的に状態の監視、NPS サーバーの構成をエクスポートして、エクスポートされた XML ファイルが含まれている、RADIUS クライアントおよびリモート RADIUS サーバー グループのメンバーの共有シークレットが暗号化されていないことを理解しています。

**管理者の資格情報**

この手順を完了するには、Administrators グループのメンバーがあります。

### <a name="to-copy-an-nps-server-configuration-to-another-nps-server-using-netsh-commands"></a>Netsh コマンドに関するページを使用して別の NPS サーバーに NPS サーバーの構成をコピーするには

1. 移行元 NPS サーバーで、開く**コマンド プロンプト**、種類**netsh**、し、Enter キーを押します。

2. **Netsh**プロンプトで、入力**nps**、し、Enter キーを押します。 

3. **Netsh nps**プロンプトで、入力**ファイル名のエクスポート =**"*path\file.xml*" **exportPSK = [はい]**ここで、*パス*NPS サーバーの構成ファイルを保存するフォルダーの場所と*ファイル*に保存する XML ファイルの名前です。 Enter キーを押します。 

構成設定を保存 \(including registry settings\) XML ファイルにします。 相対パスまたは絶対パスは、または汎用名前付け規則 \(UNC\) パスであることができます。 Enter キーを押すと、ファイルへのエクスポートが成功したかどうかを示すメッセージが表示されます。

4. 移行先 NPS サーバーに作成したファイルをコピーします。

5. 移行先 NPS サーバーでのコマンド プロンプトで次のように入力します。**netsh nps インポート filename =**"*path\file.xml*"、し、Enter キーを押します。 XML ファイルからインポートが成功したかどうかを示すメッセージが表示されます。

Netsh に関する詳細については、次を参照してください。[ネットワーク シェル (Netsh)](../netsh/netsh.md)します。

