---
title: Windows Server 2008 R2 を Windows Server 2012 R2 にアップグレードするMicrosoft Docs
description: Windows Server 2008 R2 から Windows Server 2012 R2 にインプレースアップグレードを実行する方法について説明します。
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: d5051239f7269eb4b6361187121ac960e06f6d9e
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71125082"
---
# <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>Windows Server 2008 R2 から Windows Server 2012 R2 へのアップグレード

サーバーをフラット化せずに、既に設定したものと同じハードウェアとすべてのサーバーの役割を維持する場合は、インプレースアップグレードを実行します。 インプレースアップグレードでは、設定、サーバーの役割、データをそのまま維持しながら、古いオペレーティングシステムから新しいオペレーティングシステムに移行することができます。 この記事は、Windows Server 2008 R2 から Windows Server 2012 R2 に移行する際に役立ちます。

Windows Server 2019 にアップグレードするには、このトピックを最初に使用して、Windows Server 2012 R2 にアップグレードして[から、Windows server 2012 r2 から Windows server 2019 に](upgrade-2012r2-to-2019.md)アップグレードします。

## <a name="before-you-begin-your-in-place-upgrade"></a>インプレースアップグレードを開始する前に

Windows Server のアップグレードを開始する前に、診断とトラブルシューティングのためにデバイスから情報を収集することをお勧めします。 この情報は、アップグレードが失敗した場合にのみ使用することを目的としているため、デバイスから取得できる場所に情報を保存しておく必要があります。

### <a name="to-collect-your-info"></a>情報を収集するには

1. コマンドプロンプトを開き、に`c:\Windows\system32`アクセスして、「 **systeminfo**」と入力します。

2. 生成されたシステム情報をデバイスのどこかにコピーして貼り付け、保存します。

3. コマンドプロンプトに「 **ipconfig/all** 」と入力し、結果の構成情報をコピーして、上記と同じ場所に貼り付けます。

4. レジストリエディターを開き、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion hive に移動します。次に、Windows Server **Buildlabex** (バージョン) と**EditionID** (エディション) をコピーして、上記と同じ場所に貼り付けます。

Windows Server 関連のすべての情報を収集したら、オペレーティングシステム、アプリ、および仮想マシンをバックアップすることを強くお勧めします。 また、サーバーで現在実行されているすべての仮想マシンを**シャットダウン**、**クイックマイグレーション**、または**ライブマイグレーション**する必要があります。 インプレースアップグレード中に仮想マシンを実行することはできません。

## <a name="to-perform-the-upgrade"></a>アップグレードを実行するには

1. **Buildlabex**の値に、Windows Server 2008 R2 が実行されていることが示されていることを確認します。

2. Windows Server 2012 R2 セットアップメディアを見つけて **、setup.exe を選択し**ます。

    ![Setup.exe ファイルが表示されているエクスプローラー](media/upgrade-2008r2-2012r2/setup-2012r2.png)

3. **[はい]** を選択して、セットアッププロセスを開始します。

    ![セットアップを開始するアクセス許可を要求するユーザーアカウント制御](media/upgrade-2008r2-2012r2/start-setup-uac-box.png)

4. Windows Server 2012 R2 画面で、**今すぐインストール** を選択します。

5. インターネットに接続されているデバイスの場合は、[オンラインにする] を選択して、**今すぐ更新プログラムをインストールします (推奨)** 。

    ![重要な Windows 更新プログラムを取得するためにオンラインにすることを選択する画面](media/upgrade-2008r2-2012r2/imp-updates-win-setup.png)

6. インストールする Windows Server 2012 R2 エディションを選択し、 **[次へ]** を選択します。

    ![インストールする Windows Server 2012 R2 エディションを選択する画面](media/upgrade-2008r2-2012r2/select-os-edition.png)

7. **[ライセンス条項に同意]** します を選択して、配布チャネル (、Retail、Volume LICENSE、OEM、ODM など) に基づいてライセンス契約の条項に同意し、 **[次へ]** を選択します。

    ![使用許諾契約書に同意する画面](media/upgrade-2008r2-2012r2/license-terms.png)

8. [ **アップグレード] を選択します。インプレースアップグレードを選択するには、Windows を**インストールし、ファイル、設定、およびアプリケーションを保持します。

    ![インストールの種類を選択する画面](media/upgrade-2008r2-2012r2/choose-install-upgrade.png)

9. セットアップでは、 [Windows server のインストールとアップグレード](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade)に関する記事の情報を使用して、アプリが windows Server 2012 R2 と互換性があることを確認し、 **[次へ]** を選択します。

    ![アプリの互換性を確認するようにという画面が表示される](media/upgrade-2008r2-2012r2/compatibility-report.png)

10. アップグレードを推奨しないことを示すページが表示された場合は、無視して **[確認]** を選択できます。 クリーンインストールを求めるメッセージが表示されましたが、必須ではありません。

    ![アップグレードの進行状況を示す画面](media/upgrade-2008r2-2012r2/upgrading-windows-with-progress.png)

    インプレースアップグレードが開始され、 **Windows のアップグレード**画面が進行状況と共に表示されます。 アップグレードが完了すると、サーバーが再起動します。

## <a name="after-your-upgrade-is-done"></a>アップグレードの完了後

アップグレードが完了したら、Windows Server 2012 R2 へのアップグレードが正常に完了したことを確認する必要があります。

### <a name="to-make-sure-your-upgrade-was-successful"></a>アップグレードが成功したかどうかを確認するには

1. レジストリエディターを開き、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion hive にアクセスして、 **ProductName**を表示します。 Windows server 2012 R2 のエディション ( **Windows server 2012 R2 Datacenter**など) が表示できます。

2. すべてのアプリケーションが実行されており、アプリケーションへのクライアント接続が正常に行われていることを確認します。

アップグレード中に問題が発生したと思われる場合は、 `%SystemRoot%\Panther` (通常は`C:\Windows\Panther`) ディレクトリをコピーして zip 形式にし、Microsoft サポートに問い合わせてください。

## <a name="next-steps"></a>次の手順

Windows Server 2012 R2 から Windows Server 2019 に移行するには、もう一度アップグレードを実行します。 詳細な手順については、「 [Windows server 2012 R2 から Windows server 2019 へのアップグレード](upgrade-2012r2-to-2019.md)」を参照してください。

## <a name="related-articles"></a>関連記事

- Windows Server 2012 R2 の詳細と情報については、「 [Windows server 2012 r2 および Windows server 2012](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh801901(v=ws.11))」を参照してください。
