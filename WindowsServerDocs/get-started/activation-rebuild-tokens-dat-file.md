---
title: Tokens.dat ファイルの再構築
description: Windows のライセンス認証に関する問題のトラブルシューティングを行うときに、Tokens.dat ファイルを再構築する方法
ms.topic: troubleshooting
ms.date: 09/18/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: 8a5835cd601b2eb327c8605d70bf075e6c8e8414
ms.sourcegitcommit: 9855d6b59b1f8722f39ae74ad373ce1530da0ccf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71962998"
---
# <a name="rebuild-the-tokensdat-file"></a>Tokens.dat ファイルの再構築

Windows のライセンス認証に関する問題のトラブルシューティングを行うときに、Tokens.dat ファイルを再構築することが必要になる場合があります。 この記事では、その方法について詳しく説明します。

## <a name="resolution"></a>解決方法

Tokens.dat ファイルを再構築するには、次の手順に従います。

1. 管理者特権のコマンド プロンプト ウィンドウを開きます。  
   **Windows 10 の場合**

   1. **スタート** メニューを開き、「**cmd**」と入力します。
   1. 検索結果の **[コマンド プロンプト]** を右クリックし、 **[管理者として実行]** をクリックします。  

   **Windows 8.1 の場合**
   1. 画面の右端からスワイプし、 **[検索]** をタップします。 または、マウスを使用している場合は、画面の右下隅をポイントし、 **[検索]** を選択します。
   1. 検索ボックスに「**cmd**」と入力します。
   1. 表示された **[コマンド プロンプト]** アイコンをスワイプするか、右クリックします。
   1. **[管理者として実行]** をタップまたはクリックします。

   **Windows 7 の場合**
   1. **スタート** メニューを開き、「**cmd**」と入力します。
   1. 検索結果の **[cmd.exe]** を右クリックし、 **[管理者として実行]** を選択します。

1. 使用しているオペレーティング システムに適したコマンドの一覧を入力します。  

   Windows 10、Windows Server 2016、および以降のバージョンの Windows では、次のコマンドを順番に入力します。
   ```cmd
   net stop sppsvc
   cd %windir%\system32\spp\store\2.0
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
   Windows 8.1、Windows Server 2012、Windows Server 2012 R2 の場合は、次のコマンドを順番に入力します。
   ```cmd
   net stop sppsvc
   cd %windir%\ServiceProfiles\LocalService\AppData\Local\Microsoft\WSLicense
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
   Windows 7、Windows Server 2008、Windows Server 2008 R2 の場合は、次のコマンドを順番に入力します。
   ```cmd
   net stop sppsvc
   cd %windir%\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft\SoftwareProtectionPlatform
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
1. コンピューターを再起動します。

## <a name="more-information"></a>詳細

Tokens.dat ファイルを再構築したら、次のいずれかの方法を使用してプロダクト キーを再インストールする必要があります。

- 同じ管理者特権のコマンド プロンプトで、次のコマンドを入力し、Enter キーを押します。

   ```cmd
   cscript.exe %windir%\system32\slmgr.vbs /ipk <Product key>
   ```

  > [!IMPORTANT]
  > **/upk** スイッチを使用してプロダクト キーをアンインストールしないでください。 既存のプロダクト キーにプロダクト キーを上書きインストールするには、 **/ipk** スイッチを使用します。
- **[マイ コンピューター]** を右クリックし、 **[プロパティ]** を選択します。次に、 **[プロダクト キーの変更]** を選択します。

KMS クライアント セットアップ キーの詳細については、「[KMS クライアント セットアップ キー](kmsclientkeys.md)」を参照してください。
