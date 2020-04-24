---
title: Windows Server 2012 R2 から Windows Server 2019 へのアップグレード | Microsoft Docs
description: Windows Server 2012 R2 から Windows Server 2019 に移行するためのインプレース アップグレードを実行する方法について説明します。
ms.prod: windows-server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: 02d6dd21b798346245f209174902b6f4fdf24ff8
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80853345"
---
# <a name="upgrade-windows-server-2012-r2-to-windows-server-2019"></a>Windows Server 2012 R2 から Windows Server 2019 へのアップグレード

同じハードウェアをそのまま使用し、サーバーをフラット化せずに、既に設定しているすべてのサーバーの役割を保持する場合は、インプレース アップグレードを実行します。 インプレース アップグレードでは、設定、サーバーの役割、データを保持しながら、古いオペレーティング システムから新しいものに移行できます。 この記事は、Windows Server 2012 R2 から Windows Server 2019 に移行する際に役立ちます。

## <a name="before-you-begin-your-in-place-upgrade"></a>インプレース アップグレードを開始する前に

Windows Server のアップグレードを開始する前に、診断とトラブルシューティングのためにデバイスから情報を収集することをお勧めします。 この情報は、アップグレードが失敗した場合にのみ使用することを目的としているため、デバイスからアクセスできる場所に保存しておく必要があります。

### <a name="to-collect-your-info"></a>情報を収集するには

1. コマンド プロンプトを開き、`c:\Windows\system32` に移動して、「**systeminfo.exe**」と入力します。

2. 結果として得られたシステム情報をデバイスから任意の場所にコピーして貼り付け、保存します。

3. コマンド プロンプトに「**ipconfig /all**」と入力し、結果として得られた構成情報をコピーして、上記と同じ場所に貼り付けます。

4. レジストリ エディターを開き、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion ハイブに移動して、Windows Server **BuildLabEx** (バージョン) と **EditionID** (エディション) をコピーし、上記と同じ場所に貼り付けます。

Windows Server 関連のすべての情報を収集後、オペレーティング システム、アプリ、および仮想マシンをバックアップすることを強くお勧めします。 また、サーバー上で現在実行されているすべての仮想マシンの**シャットダウン**、**クイック マイグレーション**、または**ライブ マイグレーション**を行う必要があります。 インプレース アップグレード中に仮想マシンを実行することはできません。

## <a name="to-perform-the-upgrade"></a>アップグレードを実行するには

1. **BuildLabEx** 値に、Windows Server 2012 R2 が実行中されていることが示されていることを確認します。

2. Windows Server 2019 セットアップ メディアを見つけて、**setup.exe** を選択します。

    ![setup.exe ファイルが表示されているエクスプローラー](media/upgrade-2012r2-2019/setup-2019.png)

3. **[はい]** を選択して、セットアップ プロセスを開始します。

    ![セットアップを開始するためのアクセス許可を要求するユーザー アカウント制御](media/upgrade-2012r2-2019/start-setup-uac-box.png)

4. インターネットに接続されているデバイスの場合は、 **[Download updates, drivers and optional features (recommended)]\(更新プログラム、ドライバー、オプション機能をダウンロードする (推奨)\)** オプションを選択し、 **[次へ]** を選択します。

    ![重要な Windows 更新プログラムをオンラインで取得することを選択する画面](media/upgrade-2012r2-2019/online-updates-win-setup.png)

5. デバイスの構成が確認されます。その完了を待ってから、 **[次へ]** を選択します。

6. Windows Server メディアを受け取った配布チャネル (製品版、ボリューム ライセンス、OEM、ODM など) とサーバーのライセンスによっては、続行するためにライセンス キーを入力するように求められる場合があります。

7. インストールする Windows Server 2019 エディションを選択し、 **[次へ]** を選択します。

    ![インストールする Windows Server 2012 R2 エディションを選択する画面](media/upgrade-2012r2-2019/select-os-edition.png)

8. 配布チャネル (製品版、ボリューム ライセンス、OEM、ODM など) に応じて、 **[同意する]** を選択して、ライセンス条項に同意します。

    ![ライセンス条項に同意する画面](media/upgrade-2012r2-2019/license-terms.png)

9. セットアップにより、 **[プログラムの追加と削除]** を使用して Microsoft Endpoint Protection を削除することが推奨されます。

    この機能は、Windows Server 2019 と互換性がありません。

10. **[個人用ファイルとアプリを引き継ぐ]** を選択して、インプレース アップグレードを行うことを選択し、 **[次へ]** を選択します。

    ![インストールの種類を選択する画面](media/upgrade-2012r2-2019/choose-install-upgrade.png)

11. セットアップによるデバイスの分析後、 **[インストール]** を選択してアップグレードを進めるように求められます。

    ![アップグレードを開始する準備ができていることを示す画面](media/upgrade-2012r2-2019/ready-to-install.png)

    インプレース アップグレードが開始され、進行状況を示す **[Windows をアップグレードしています]** 画面が表示されます。 アップグレードが完了すると、サーバーが再起動します。

    ![アップグレードの進行状況を表示している画面](media/upgrade-2012r2-2019/upgrading-windows-with-progress.png)

## <a name="after-your-upgrade-is-done"></a>アップグレードの完了後

アップグレードの完了後、Windows Server 2019 へのアップグレードが成功したことを確認する必要があります。

### <a name="to-make-sure-your-upgrade-was-successful"></a>アップグレードが成功したかどうかを確認するには

1. レジストリ エディターを開き、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion ハイブに移動して、**ProductName** を表示します。 **Windows Server 2019 Datacenter** など、Windows Server 2019 のエディションが表示されるはずです。

2. すべてのアプリケーションが実行されており、アプリケーションへのクライアント接続が正常に行われていることを確認します。

アップグレード中に問題が発生したと思われる場合は、`%SystemRoot%\Panther` (通常は `C:\Windows\Panther`) ディレクトリをコピーして zip 圧縮し、Microsoft サポートにお問い合わせください。

## <a name="related-articles"></a>関連記事

- Windows Server 2019 に関する情報と詳細については、「[Windows Server 2019 の概要](https://docs.microsoft.com/windows-server/get-started-19/get-started-19)」を参照してください。