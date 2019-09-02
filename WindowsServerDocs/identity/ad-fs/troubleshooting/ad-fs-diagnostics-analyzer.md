---
title: AD FS ヘルプ診断アナライザー
description: このドキュメントでは、AD FS Help Diagnostics Analyzer と、AD FS 診断 PowerShell モジュールを使用して基本的なチェックを実行する方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.reviewer: anandyadavMSFT
ms.date: 03/29/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6b6b7563aaa1f3c7d706cfdd172faf18417623e5
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546579"
---
# <a name="ad-fs-help-diagnostics-analyzer"></a>AD FS ヘルプ診断アナライザー

AD FS には、認証とアプリケーションの開発のために提供するさまざまな機能をサポートする多くの設定があります。 トラブルシューティングの際には、すべての AD FS 設定が正しく構成されていることを確認することをお勧めします。 これらの設定を手動でチェックすると、時間がかかることがあります。 AD FS Help Diagnostics Analyzer は、ADFSToolbox PowerShell モジュールを使用して基本的なチェックを実行するのに役立ちます。 このチェックを実行すると、結果を簡単に視覚化して修復手順を提示するのに役立つ[診断アナライザー](https://aka.ms/adfsdiagnosticsanalyzer)が AD FS ヘルプに表示されます。

Complete 操作では、次の3つの簡単な手順が実行されます。

1. プライマリ AD FS サーバーまたは WAP サーバーで ADFSToolbox モジュールをセットアップする
2. 診断を実行し、ファイルを AD FS ヘルプにアップロードします
3. 診断分析を表示し、問題を解決する

トラブルシューティングを開始するには、 [AD FS ヘルプ診断アナライザー https://aka.ms/adfsdiagnosticsanalyzer) ](https://aka.ms/adfsdiagnosticsanalyzer)にアクセスしてください。

![AD FS ヘルプの AD FS diagnostics analyzer ツール](media/ad-fs-diagonostics-analyzer/home.png)

## <a name="step-1-setup-the-adfstoolbox-module-on-ad-fs-server"></a>手順 1:AD FS サーバーでの ADFSToolbox モジュールのセットアップ

[診断アナライザー](https://aka.ms/adfsdiagnosticsanalyzer)を実行するには、ADFSToolbox PowerShell モジュールをインストールする必要があります。 AD FS サーバーがインターネットに接続できる場合は、PowerShell ギャラリーから ADFSToolbox モジュールを直接インストールできます。 インターネットに接続されていない場合は、手動でインストールすることができます。 

[!WARNING]
AD FS 2.1 以下を使用している場合は、ADFSToolbox のバージョン1.0.13 をインストールする必要があります。 ADFSToolbox では、最新バージョンで AD FS 2.1 以降がサポートされなくなりました。

![AD FS diagnostics analyzer-セットアップ](media/ad-fs-diagonostics-analyzer/step1_v2.png)

### <a name="setup-using-powershell-gallery"></a>PowerShell ギャラリーを使用したセットアップ

AD FS サーバーがインターネットに接続されている場合は、次に示す PowerShell コマンドを使用して、PowerShell ギャラリーから ADFSToolbox モジュールを直接インストールすることをお勧めします。

   ```powershell
    Install-Module -Name ADFSToolbox -force
    Import-Module ADFSToolbox -force
   ```

### <a name="setup-manually"></a>手動によるセットアップ

ADFSToolbox モジュールは、AD FS または WAP サーバーに手動でコピーする必要があります。 次の手順に従います。

1. インターネットにアクセスできるコンピューターで、管理者特権の PowerShell ウィンドウを起動します。
2. AD FS ツールボックスモジュールをインストールします。

    ```powershell
    Install-Module -Name ADFSToolbox -Force
    ```
3. ローカルコンピューターにある`%SYSTEMDRIVE%\Program Files\WindowsPowerShell\Modules\` adfstoolbox フォルダーを、AD FS または WAP コンピューターの同じ場所にコピーします。

4. AD FS マシンで管理者特権の PowerShell ウィンドウを起動し、次のコマンドレットを実行してモジュールをインポートします。

    ```powershell
    Import-Module ADFSToolbox -Force
    ```

## <a name="step-2-execute-the-diagnostics-cmdlet"></a>手順 2:診断コマンドレットを実行する

![AD FS diagnostics analyzer ツール-実行とアップロードの結果](media/ad-fs-diagonostics-analyzer/step2_v2.png)

1つのコマンドを使用して、ファーム内のすべての AD FS サーバーで診断テストを簡単に実行できます。 PowerShell モジュールは、リモート PS セッションを使用して、ファーム内のさまざまなサーバーに対して診断テストを実行します。

```powershell
    Export-AdfsDiagnosticsFile [-ServerNames <list of servers>]
```

サーバー2016以上の AD FS ファームでは、コマンドは AD FS 構成から AD FS サーバーの一覧を読み取ります。 その後、一覧内の各サーバーに対して診断テストが試行されます。 AD FS サーバーの一覧 (例 2012R2) が使用できない場合は、ローカルコンピューターに対してテストが実行されます。 テストを実行する対象のサーバーの一覧を指定するには、 **Servernames**引数を使用してサーバーの一覧を指定します。 次に例を示します。

```powershell
    Export-AdfsDiagnosticsFile -ServerNames @("adfs1.contoso.com", "adfs2.contoso.com")
```

結果として、コマンドを実行したディレクトリに作成された JSON ファイルが生成されます。 ファイルの名前は AdfsDiagnosticsFile\<\>です。 ファイル名の例は、AdfsDiagnosticsFile-07312019-184201 です。

## <a name="step-3-upload-the-diagnostics-file"></a>手順 3:診断ファイルをアップロードする

「」の[https://aka.ms/adfsdiagnosticsanalyzer](https://aka.ms/adfsdiagnosticsanalyzer)手順3では、ファイルブラウザーを使用して、アップロードする結果ファイルを選択します。

**[アップロード]** をクリックしてアップロードを完了します。

Microsoft アカウントでサインインすることにより、診断結果を後で表示するために保存し、Microsoft サポートに送信できます。 サポートケースを開いた時点で、Microsoft は診断アナライザーの結果を表示し、問題のトラブルシューティングを迅速に行うことができます。

![AD FS diagnostics analyzer ツール-サインイン](media/ad-fs-diagonostics-analyzer/sign_in_step.png)

## <a name="step-4-view-diagnostics-analysis-and-resolve-any-issues"></a>手順 4:診断分析を表示し、問題を解決する

テスト結果には、次の5つのセクションがあります。

1. ［失敗］:このセクションには、失敗したテストの一覧が含まれています。 各結果は次のもので構成します。
2. 警告 :このセクションには、警告が発生したテストの一覧が含まれています。 これらの問題によって、より広範な規模で認証に関する問題が発生する可能性はほとんどありませんが、最も早い段階で対処する必要があります。
3. 渡しこのセクションには、合格したテストのうち、ユーザーに対してアクション項目がないテストの一覧が含まれています。
4. 実行しない:このセクションには、情報が不足しているために実行できなかったテストの一覧が含まれています。
5. 適用外:このセクションには、コマンドが実行されていた特定のサーバーに適用できなかったために実行されなかったテストの一覧が含まれています。

![AD FS diagnostics analyzer ツール-テスト結果一覧](media/ad-fs-diagonostics-analyzer/step3a_v3.png)には、テストとその解決策について説明する詳細情報が表示されます。

1. テスト名:実行されたテストの名前
2. 説明:テストの説明。
3. 詳細:テスト中に実行された操作全体の説明
4. 解決手順:テストで強調表示されている問題を解決するために推奨される手順

![AD FS diagnostics analyzer ツール-障害解決](media/ad-fs-diagonostics-analyzer/step3b_v3.png)

## <a name="next"></a>Next

- [AD FS Help troublehshooting ガイドを使用する](https://aka.ms/adfshelp/troubleshooting )
- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)
