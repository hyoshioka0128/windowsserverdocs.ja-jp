---
title: Windows Server 2008 R2 から Windows Server 2012 R2 へのアップグレード | Microsoft Docs
description: Windows Server 2008 R2 から Windows Server 2012 R2 に移行するためのインプレース アップグレードを実行する方法について説明します。
ms.prod: windows-server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: 7598826bee4abd869dff82c3891fdbe126db35fb
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182178"
---
# <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>Windows Server 2008 R2 から Windows Server 2012 R2 へのアップグレード

同じハードウェアをそのまま使用し、サーバーをフラット化せずに、既に設定しているすべてのサーバーの役割を保持する場合は、インプレース アップグレードを実行します。 インプレース アップグレードでは、設定、サーバーの役割、データを保持しながら、古いオペレーティング システムから新しいものに移行できます。 この記事は、Windows Server 2008 R2 から Windows Server 2012 R2 に移行する際に役立ちます。

Windows Server 2019 にアップグレードするには、まずこのトピックを使用して Windows Server 2012 R2 にアップグレードしてから、[Windows Server 2012 R2 から Windows Server 2019 にアップグレードします](upgrade-2012r2-to-2019.md)。

## <a name="before-you-begin-your-in-place-upgrade"></a>インプレース アップグレードを開始する前に

Windows Server のアップグレードを開始する前に、診断とトラブルシューティングのためにデバイスから情報を収集することをお勧めします。 この情報は、アップグレードが失敗した場合にのみ使用することを目的としているため、デバイスからアクセスできる場所に保存しておく必要があります。

### <a name="to-collect-your-info"></a>情報を収集するには

1. コマンド プロンプトを開き、`c:\Windows\system32` に移動して、「**systeminfo.exe**」と入力します。

2. 結果として得られたシステム情報をデバイスから任意の場所にコピーして貼り付け、保存します。

3. コマンド プロンプトに「**ipconfig /all**」と入力し、結果として得られた構成情報をコピーして、上記と同じ場所に貼り付けます。

4. レジストリ エディターを開き、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion ハイブに移動して、Windows Server **BuildLabEx** (バージョン) と **EditionID** (エディション) をコピーし、上記と同じ場所に貼り付けます。

Windows Server 関連のすべての情報を収集後、オペレーティング システム、アプリ、および仮想マシンをバックアップすることを強くお勧めします。 また、サーバー上で現在実行されているすべての仮想マシンの**シャットダウン**、**クイック マイグレーション**、または**ライブ マイグレーション**を行う必要があります。 インプレース アップグレード中に仮想マシンを実行することはできません。

## <a name="to-perform-the-upgrade"></a>アップグレードを実行するには

1. **BuildLabEx** 値に、Windows Server 2008 R2 が実行中されていることが示されていることを確認します。

2. Windows Server 2012 R2 セットアップ メディアを見つけて、**setup.exe** を選択します。

    ![setup.exe ファイルが表示されているエクスプローラー](media/upgrade-2008r2-2012r2/setup-2012r2.png)

3. **[はい]** を選択して、セットアップ プロセスを開始します。

    ![セットアップを開始するためのアクセス許可を要求するユーザー アカウント制御](media/upgrade-2008r2-2012r2/start-setup-uac-box.png)

4. Windows Server 2012 R2 の画面で、 **[今すぐインストール]** を選択します。

5. インターネットに接続されているデバイスの場合は、 **[オンラインで今すぐ更新プログラムをインストールする (推奨)]** を選択します。

    ![重要な Windows 更新プログラムをオンラインで取得することを選択する画面](media/upgrade-2008r2-2012r2/imp-updates-win-setup.png)

6. インストールする Windows Server 2012 R2 エディションを選択し、 **[次へ]** を選択します。

    ![インストールする Windows Server 2012 R2 エディションを選択する画面](media/upgrade-2008r2-2012r2/select-os-edition.png)

7. 配布チャネル (製品版、ボリューム ライセンス、OEM、ODM など) に応じて、 **[同意します]** を選択してライセンス条項に同意し、 **[次へ]** を選択します。

    ![ライセンス条項に同意する画面](media/upgrade-2008r2-2012r2/license-terms.png)

8. **[Upgrade:Install Windows and keep files, settings, and applications]\(アップグレード: Windows をインストールし、ファイル、設定、アプリを引き継ぐ\)** を選択して、インプレース アップグレードを行うことを選択します。

    ![インストールの種類を選択する画面](media/upgrade-2008r2-2012r2/choose-install-upgrade.png)

9. セットアップから、「[Windows Server のインストールとアップグレード](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade)」の記事に記載されている情報を使用してアプリが Windows Server 2012 R2 と互換性があることを確認してから **[次へ]** を選択するよう促されます。

    ![アプリの互換性を確認するよう促す画面](media/upgrade-2008r2-2012r2/compatibility-report.png)

10. アップグレードが推奨されないことを示すページが表示された場合、これを無視して **[確認]** を選択することができます。 これはクリーン インストールを促すために導入されたものですが、必須ではありません。

    ![アップグレードの進行状況を表示している画面](media/upgrade-2008r2-2012r2/upgrading-windows-with-progress.png)

    インプレース アップグレードが開始され、進行状況を示す **[Windows をアップグレードしています]** 画面が表示されます。 アップグレードが完了すると、サーバーが再起動します。

## <a name="after-your-upgrade-is-done"></a>アップグレードの完了後

アップグレードの完了後、Windows Server 2012 R2 へのアップグレードが成功したことを確認する必要があります。

### <a name="to-make-sure-your-upgrade-was-successful"></a>アップグレードが成功したかどうかを確認するには

1. レジストリ エディターを開き、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion ハイブに移動して、**ProductName** を表示します。 **Windows Server 2012 R2 Datacenter** など、Windows Server 2012 R2 のエディションが表示されるはずです。

2. すべてのアプリケーションが実行されており、アプリケーションへのクライアント接続が正常に行われていることを確認します。

アップグレード中に問題が発生したと思われる場合は、`%SystemRoot%\Panther` (通常は `C:\Windows\Panther`) ディレクトリをコピーして zip 圧縮し、Microsoft サポートにお問い合わせください。

## <a name="next-steps"></a>次の手順

Windows Server 2012 R2 から Windows Server 2019 に移行するもう 1 つのアップグレードを実行できます。 詳細な手順については、「[Windows Server 2012 R2 から Windows Server 2019 へのアップグレード](upgrade-2012r2-to-2019.md)」を参照してください。

## <a name="related-articles"></a>関連記事

- Windows Server 2012 R2 に関する情報と詳細については、「[Windows Server 2012 R2 および Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh801901(v=ws.11))」を参照してください。
