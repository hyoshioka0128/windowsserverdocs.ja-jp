---
title: AD FS ヘルプ診断アナライザー
description: このドキュメントが AD FS ヘルプ診断アナライザーをについて説明し、AD FS 診断モジュールを PowerShell を使用して基本的なを実行できる方法を確認します。
author: billmath
ms.author: billmath
manager: mtillman
ms.reviewer: anandyadavMSFT
ms.date: 03/29/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8d9acd1adcb8d9566b154abfef940e21609a6684
ms.sourcegitcommit: 4ff3d00df3148e4bea08056cea9f1c3b52086e5d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64773371"
---
# <a name="ad-fs-help-diagnostics-analyzer"></a>AD FS ヘルプ診断アナライザー

AD FS では、さまざまな認証とアプリケーションの開発を提供する機能をサポートする多数の設定があります。 トラブルシューティング時に、すべての AD FS の設定が正しく構成されていることを確認することをお勧めします。 これらの設定の手動のチェックを行う場合があります時間がかかります。 AD FS ヘルプ診断アナライザーが ADFSToolbox PowerShell モジュールを使用して基本的なチェックを実行できます。 AD FS ヘルプは、チェックを実行した後、[診断アナライザー](https://aka.ms/adfsdiagnosticsanalyzer)簡単に結果を視覚化および修復手順を提供するためです。

完了操作は簡単な 3 ステップを受け取ります。

1. プライマリ AD FS サーバー上で WAP サーバー ADFSToolbox モジュールをセットアップします。
2. 診断を実行し、AD FS ヘルプ ファイルをアップロード
3. 診断の分析を表示し、問題を解決

移動して[AD FS ヘルプ診断アナライザー (https://aka.ms/adfsdiagnosticsanalyzer) ](https://aka.ms/adfsdiagnosticsanalyzer)トラブルシューティングを開始します。

![AD FS ヘルプの AD FS 診断アナライザー ツール](media/ad-fs-diagonostics-analyzer/home.png)

## <a name="step-1-setup-the-adfstoolbox-module-on-ad-fs-server"></a>手順 1:AD FS サーバーで ADFSToolbox モジュールをセットアップします。

実行する、[診断アナライザー](https://aka.ms/adfsdiagnosticsanalyzer)、ADFSToolbox PowerShell モジュールをインストールする必要があります。 AD FS サーバーにインターネットへの接続がある場合は、PowerShell ギャラリーから直接 ADFSToolbox モジュールをインストールできます。 インターネットに接続されていないが発生した場合に、手動でインストールの GitHub リポジトリを複製します。

![AD FS 診断アナライザーのセットアップ](media/ad-fs-diagonostics-analyzer/step1.png)

### <a name="setup-using-powershell-gallery"></a>PowerShell ギャラリーを使用した設定します。

AD FS サーバーにインターネット接続がある場合は、次の PowerShell コマンドを使用して PowerShell ギャラリーから直接 ADFSToolbox モジュールをインストールすることをお勧めします。

   ```powershell
    Install-Module -Name ADFSToolbox -force
    Import-Module ADFSToolbox -force
   ```
### <a name="setup-manually-by-cloning-the-repository"></a>リポジトリを複製することにより手動でセットアップします。

ADFSToolbox モジュールは手動でインストールする GitHub から直接します。 リポジトリを複製して、AD FS サーバーで ADFSToolbox モジュールをインストールするための以下の手順に従います。

1. ダウンロード、[リポジトリ](https://github.com/Microsoft/adfsToolbox/archive/master.zip)
2. ダウンロードしたファイルを解凍し、%systemdrive% adfsToolbox マスター フォルダーにコピー\\Program Files\\WindowsPowerShell\\モジュール\\します。
3. PowerShell モジュールをインポートします。 管理者特権の PowerShell ウィンドウで、次の手順を実行します。

   ```powershell
    Import-Module ADFSToolbox -Force
   ```

## <a name="step-2-execute-the-diagnostics-and-upload-the-file-to-ad-fs-help"></a>手順 2:診断を実行し、AD FS ヘルプ ファイルをアップロード

簡単に、ファーム内のすべての AD FS サーバー間で、診断テストを実行する 1 つのコマンドを使用できます。 PowerShell モジュールは、ファーム内の別のサーバー間で、診断テストを実行するのにリモート PS セッションを使用します。

```powershell
    Export-AdfsDiagnosticsFile [-adfsServers <list of servers>]
```

Server 2016 の AD FS ファームで、コマンドは、AD FS の構成から、AD FS サーバーの一覧を読み取ります。 診断テストは、一覧内の各サーバーに対して試行されます。 かどうかは AD FS サーバーの一覧は使用できません (例 2012R2) し、ローカル マシンに対してテストを実行します。 テストが実行される対象となるサーバーの一覧を指定するには、使用、 **adfsServers**サーバーの一覧を提供する引数。 例を次に示します

```powershell
    Export-AdfsDiagnosticsFile -adfsServers @("sts1.contoso.com", "sts2.contoso.com", "sts3.contoso.com")
```

コマンドが実行されたのと同じディレクトリに作成されている JSON ファイルになります。 ファイルの名前は ADFSDiagnosticsFile -\<タイムスタンプ\>します。 ファイル名の例は、ADFSDiagnosticsFile 20180716124030 です。

手順 2 で[ https://aka.ms/adfsdiagnosticsanalyzer ](https://aka.ms/adfsdiagnosticsanalyzer)ファイル ブラウザーを使用してアップロードする結果ファイルを選択します。

![AD FS 診断アナライザー ツールの実行し、結果のアップロード](media/ad-fs-diagonostics-analyzer/step2.png)

をクリックして**アップロード**アップロードを完了し、次の手順に移動します。


Microsoft アカウントをサインインすることで結果を保存して後で表示するポイント、および Microsoft に送信できる診断をサポートします。 任意のポイントが、サポート ケースを開く場合に Microsoft は診断アナライザーの結果を表示したり、問題を迅速に解決することになります。

![AD FS 診断アナライザー ツール - サインイン](media/ad-fs-diagonostics-analyzer/sign_in_step.png)

## <a name="step-3-view-diagnostics-analysis-and-resolve-any-issues"></a>手順 3:診断の分析を表示し、問題を解決

これには、テスト結果の 4 つのセクションがあります。

1. ［失敗］:このセクションには、失敗したテストの一覧が含まれています。 各結果で構成されます。
2. 警告:このセクションには、警告を発生させたがテストのリストが含まれています。 これらの問題より広範なスケールでの認証に関するすべての問題でない可能性しますが、できるだけ早く対処する必要があります。
3. 適用外:このセクションには、コマンドを実行していた特定のサーバーに適用されなかったために実行されなかったテストの一覧が含まれています。
4. 渡されます。このセクションには、渡される、ユーザーのアクション アイテムはありませんが、テストの一覧が含まれています。

![AD FS 診断アナライザー ツールのテスト結果のリスト](media/ad-fs-diagonostics-analyzer/step3a_v2.png)テストと解決方法の手順を説明する詳細と共に各テスト結果が表示されます。

1. テスト名:実行されたテストの名前
2. 詳細:テスト中に実行された全体的な操作の説明
3. 解決手順:テストで強調表示されている問題を解決する推奨される手順

![AD FS 診断アナライザー ツールのエラーの解決](media/ad-fs-diagonostics-analyzer/step3b_v2.png)

## <a name="next"></a>Next

- [AD FS ヘルプ troublehshooting ガイドを使用してください。](https://aka.ms/adfshelp/troubleshooting )
- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)
