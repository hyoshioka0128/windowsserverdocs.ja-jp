---
title: Windows Server 2016 を Windows Server 2019 にアップグレードするMicrosoft Docs
description: インプレースアップグレードを実行して Windows Server 2016 から Windows Server 2019 に移行する方法について説明します。
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: 99133f2c582b180f240740fc2f39e99527bc0cf8
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71124822"
---
# <a name="upgrade-windows-server-2016-to-windows-server-2019"></a>Windows Server 2016 を Windows Server 2019 にアップグレードする

サーバーをフラット化せずに、既に設定したものと同じハードウェアとすべてのサーバーの役割を維持する場合は、インプレースアップグレードを実行します。 インプレースアップグレードでは、設定、サーバーの役割、データをそのまま維持しながら、古いオペレーティングシステムから新しいオペレーティングシステムに移行することができます。 この記事では、Windows Server 2016 から Windows Server 2019 に移行する方法について説明します。

## <a name="before-you-begin-your-in-place-upgrade"></a>インプレースアップグレードを開始する前に

Windows Server のアップグレードを開始する前に、診断とトラブルシューティングのためにデバイスから情報を収集することをお勧めします。 この情報は、アップグレードが失敗した場合にのみ使用することを目的としているため、デバイスから取得できる場所に情報を保存しておく必要があります。

### <a name="to-collect-your-info"></a>情報を収集するには

1. コマンドプロンプトを開き、に`c:\Windows\system32`アクセスして、「 **systeminfo**」と入力します。

2. 生成されたシステム情報をデバイスのどこかにコピーして貼り付け、保存します。

3. コマンドプロンプトに「 **ipconfig/all** 」と入力し、結果の構成情報をコピーして、上記と同じ場所に貼り付けます。

4. レジストリエディターを開き、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion hive に移動します。次に、Windows Server **Buildlabex** (バージョン) と**EditionID** (エディション) をコピーして、上記と同じ場所に貼り付けます。

Windows Server 関連のすべての情報を収集したら、オペレーティングシステム、アプリ、および仮想マシンをバックアップすることを強くお勧めします。 また、サーバーで現在実行されているすべての仮想マシンを**シャットダウン**、**クイックマイグレーション**、または**ライブマイグレーション**する必要があります。 インプレースアップグレード中に仮想マシンを実行することはできません。

## <a name="to-perform-the-upgrade"></a>アップグレードを実行するには

1. **Buildlabex**値に、Windows Server 2016 を実行していることが示されていることを確認します。

2. Windows Server 2019 セットアップメディアを見つけて、 **setup.exe**を選択します。

    ![Setup.exe ファイルが表示されているエクスプローラー](media/upgrade-2016-2019/setup-2019.png)

3. **[はい]** を選択して、セットアッププロセスを開始します。

    ![セットアップを開始するアクセス許可を要求するユーザーアカウント制御](media/upgrade-2016-2019/start-setup-uac-box.png)

4. インターネットに接続されているデバイスの場合は、 **[更新プログラム、ドライバー、およびオプション機能をダウンロードする (推奨)]** オプションを選択し、 **[次へ]** を選択します。

    ![重要な Windows 更新プログラムを取得するためにオンラインにすることを選択する画面](media/upgrade-2016-2019/online-updates-win-setup.png)

5. デバイスの構成が確認され、完了するのを待ってから **[次へ]** を選択します。

6. から Windows Server メディアを受信した配布チャネル (製品版、ボリュームライセンス、OEM、ODM など) とサーバーのライセンスに応じて、ライセンスキーを入力して続行するように求められる場合があります。

7. インストールする Windows Server 2019 エディションを選択し、 **[次へ]** を選択します。

    ![インストールする Windows Server 2016 エディションを選択する画面](media/upgrade-2016-2019/select-os-edition.png)

8. 配布チャネル (、Retail、Volume License、OEM、ODM など) に基づいて、ライセンス契約の条項に同意するには、[**同意**する] を選択します。

    ![使用許諾契約書に同意する画面](media/upgrade-2016-2019/license-terms.png)

9. **[個人用ファイルとアプリを保持]** する を選択してインプレースアップグレードを選択し、 **[次へ]** を選択します。

    ![インストールの種類を選択する画面](media/upgrade-2016-2019/choose-install-upgrade.png)

10. セットアップによってデバイスが分析されると、 **[インストール]** を選択してアップグレードを続行するように求められます。

    ![アップグレードを開始する準備ができていることを示す画面](media/upgrade-2016-2019/ready-to-install.png)

    インプレースアップグレードが開始され、 **Windows のアップグレード**画面が進行状況と共に表示されます。 アップグレードが完了すると、サーバーが再起動します。

    ![アップグレードの進行状況を示す画面](media/upgrade-2016-2019/upgrading-windows-with-progress.png)

## <a name="after-your-upgrade-is-done"></a>アップグレードの完了後

アップグレードが完了したら、Windows Server 2019 へのアップグレードが正常に完了したことを確認する必要があります。

### <a name="to-make-sure-your-upgrade-was-successful"></a>アップグレードが成功したかどうかを確認するには

1. レジストリエディターを開き、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion hive にアクセスして、 **ProductName**を表示します。 Windows server **2019 Datacenter**などの windows server 2019 のエディションが表示するはずです。

2. すべてのアプリケーションが実行されており、アプリケーションへのクライアント接続が正常に行われていることを確認します。

アップグレード中に問題が発生したと思われる場合は、 `%SystemRoot%\Panther` (通常は`C:\Windows\Panther`) ディレクトリをコピーして zip 形式にし、Microsoft サポートに問い合わせてください。

## <a name="related-articles"></a>関連記事

- Windows Server 2019 の詳細と情報については、「 [Windows server 2019 の概要](https://docs.microsoft.com/windows-server/get-started-19/get-started-19)」を参照してください。