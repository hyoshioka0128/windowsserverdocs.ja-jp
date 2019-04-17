---
title: "セットアップ時のアドインのインストールを自動化します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e6ff6e4-8d68-4d49-9e38-8088bc8bf95e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d4c547c2fec8e2b11e5c1d9bde46e55e91c9d6fa
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="automate-installation-of-add-ins-during-setup"></a>セットアップ時のアドインのインストールを自動化します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

##  <a name="BKMK_AddIns"></a>セットアップ時にアドインのインストールを自動化します。  
 セットアップ時にアドインをインストールするで説明されている PostIC.cmd メソッドを使用して、[後の初期構成タスクを実行している PostIC.cmd ファイルを作成する](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md)このドキュメントの「します。  
  
 次のエントリを PostIC.cmd に追加します。  
  
```  
C:\Program Files\Windows Server\bin\Installaddin.exe <full path to wssx file> -q  
```  
  
 アドインのインストール前とカスタマイズされたアンインストール手順になりました。  
  
 プレインストール手順はすべてをインストールする前に実行**.msi** addin.xml で指定されたファイルです。 対話モードで実行すると、進行状況ダイアログなります示されているが、進行状況を変更することがなく。 プレインストール フェーズ中に、取り消しボタンは無効です。 プレインストール手順を実装するには、(パッケージ直下の addin.xml で、次の内容を追加します。  
  
> [!NOTE]
>  Xml スキーマは、次に厳密に従う必要があります。  
  
```  
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">  
  <Id>...</Id>  
  <Version>...</Version>  
  <Name>...</Name>  
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>  
  <ServerBinary>...</ServerBinary>  
  <ClientBinary32>...</ClientBinary32>  
  <ClientBinary64>...</ClientBinary64>  
  <SupportedSkus>...</SupportUrl>    
  <SupportUrl>...</SupportUrl>  
  <Location>...</Location>    
  <PrivacyStatement>...</PrivacyStatement>  
  <OtherBinaries>...</OtherBinaries>   
  <Preinstall>  
<Executable>exefile</Executable>  
<NormalArgs>args-for-interactive-mode</NormalArgs>  
<SilentArgs>args-for-silent-mode</SilentArgs>  
<IgnoreExitCode>true</IgnoreExitCode>  
  </Preinstall>  
  <UninstallConfirm>...</UninstallConfirm>      
</Package>  
<¦>  
<¦>  
```  
  
 Wherein **exefile**実行可能ファイル、インストール前の手順を実行する追加のパッケージでは、指定する必要があります。 **NormalArgs**モードの場合に、対話型コマンド ラインで exefile に渡される引数を使用するかを指定します。 このモードでは、exefile ことができますポップアップ中におけるダイアログのユーザーの操作します。 **SilentArgs**モードの場合に、サイレント コマンド ラインで exefile に渡される引数を使用を指定します (-installaddin.exe を起動する場合は-q を指定) します。 Exefile には、このモードで任意の windows ポップアップしないする必要があります。 場合**IgnoreExitCode**プレインストール手順は常に成功と見なされます、それ以外の場合、成功を示す終了コード 0、1 は、取り消しを示しますおよびその他の値がエラーを示す true の場合で指定します。 タグ**NormalArgs**、**SilentArgs**、および**IgnoreExitCode**はすべてオプションです。  
  
 カスタマイズされたアンインストール手順は、次のいずれにも使用できます。  
  
-   組み込みの確認ダイアログを置換します。  
  
-   アンインストールする前にカスタマイズされたダイアログ ボックスを設定します。  
  
-   アンインストール前に、の特定のタスクを実行します。  
  
 アンインストール手順を実装するには、(パッケージ直下の addin.xml で、次の内容を追加します。  
  
```  
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">  
  <Id>...</Id>  
  <Version>...</Version>  
  <Name>...</Name>  
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>  
  <ServerBinary>...</ServerBinary>  
  <ClientBinary32>...</ClientBinary32>  
  <ClientBinary64>...</ClientBinary64>  
  <SupportedSkus>...</SupportUrl>    
  <SupportUrl>...</SupportUrl>  
  <Location>...</Location>    
  <PrivacyStatement>...</PrivacyStatement>  
  <OtherBinaries>...</OtherBinaries>   
  <Preinstall>¦</Preinstall>  
<UninstallConfirm>  
<Executable>full-path-to-exefile</Executable>  
<Arguments>command-line-arguments</Arguments>  
</UninstallConfirm>  
</Package>  
```  
  
 Wherein**完全パスを exefile**システムに既にインストールされている exefile を指定します。 **引数**オプションであり、exefile のコマンド ライン引数を指定します。 Exefile が呼び出されるは、組み込みのアンインストールの確認前にダイアログが表示されます。  
  
 Exefile は、このフェーズで次のタスク実行できます。  
  
-   ユーザーの操作の一部のダイアログが表示されます。  
  
-   一部のバック グラウンド タスクを実行します。  
  
 この実行可能ファイルの終了コードは、アンインストール プロセスがどのように移動を確認します。  
  
-   0: ユーザーは、既に確認済みのと同じように、組み込みの確認ダイアログを入力せずアンインストール処理が続行します。 (このアプローチは、組み込みの確認ダイアログの置換に使用できます。)  
  
-   1: アンインストール プロセスは取り消され、最後に、取り消しのメッセージはユーザーに表示されます。 すべての設定が変更されていません。  
  
-   その他: アンインストール プロセスを続行組み込みの確認ダイアログ ボックスで、カスタマイズされたアンインストール手順が存在しないと同様です。  
  
 Exefile の起動に失敗したは、0 または 1 以外のコードを返した場合と、同じ動作につながります。  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)