---
title: 複数言語のクライアント復元メディアの作成
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 2fdbc016-d464-43cb-bd75-8a63e61588a2
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 4057e0d6805c7633bf07960d06d97b2eab15f28a
ms.sourcegitcommit: 04637054de2bfbac66b9c78bad7bf3e7bae5ffb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87838091"
---
# <a name="build-multi-language-client-restore-media"></a>複数言語のクライアント復元メディアの作成

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

> [!NOTE]
>  まず、「[チュートリアル:](/previous-versions/windows/it-pro/windows-8.1-and-8/jj126995(v=win.10)) Windows Server Essentials install.wim pack をインストールする前に、多言語 windows イメージの作成」の説明に従って、多言語の windows イメージを作成する必要があります。

 複数言語のサーバー インストール DVD を作成すると、サーバーの install.wim に言語パックがインストールされます。 言語パックの一部として、復元ウィザードのローカライズされたリソースがインストールされます。

### <a name="to-build-a-multi-language-client-restore-media"></a>複数言語のクライアント復元メディアを作成するには

1.  c:\mount に install.wim をマウントします (以下では、c:\mount\Program Files\Windows Server\bin\ClientRestore フォルダーを、クライアント復元メディアのルートとして、[RestoreMediaRoot] と記述します)。

    ```
    dism /mount-wim /wimfile:install.wim /index:1 /mountdir:c:\mount
    ```

2.  [RestoreMediaRoot]\Sources\Boot.wim にクライアント復元 WIM ファイルをマウントします (boot_x86.wim でも同じ手順を実行する必要があります)。 コマンド ラインは次のとおりです。

    ```
    dism /mount-wim /wimfile:boot.wim /index:1 /mountdir:c:\mountRestore
    ```

3.  次の手順を実行して、復元メディアに WinPE-Setup.cab パッケージを追加します。

    ```
    dism /image:c:\mountRestore /add-package /packagepath:WinPE-Setup.cab
    ```

4.  メモ帳を使用して c:\mountRestore\windows\system32\winpeshl.ini を編集し、次の内容を指定します。

    ```
    [LaunchApp]
    AppPath = %SYSTEMDRIVE%\sources\SelectLanguage.exe
    ```

5.  復元メディアに言語パックを追加します。 次のコマンドを実行して言語パックを追加します。

    ```
    dism /image:c:\mountRestore /add-package /packagepath:[language pack path]
    ```

     次の言語パックを追加する必要があります。

    1.  WinPE 言語パック (lp.cab)

    2.  WinPE-Setup 言語パック (WinPE-Setup_[lang].cab。たとえば、WinPE-Setup_en-us.cab など)

    3.  zh-cn、zh-tw、zh-hk、ko-kr、ja-jp などのアジア系言語用フォントの場合、追加のフォント パックをインストールする必要があります (winpe-fontsupport-zh-cn.cab などの winpe-fontsupport-[lang].cab)

6.  次の手順を実行して、新しい Lang.ini ファイルを生成します。

    ```
    dism /image:c:\mountRestore /Gen-LangINI /distribution:mount
    ```

7.  次の手順を実行して、イメージのコミットとマウント解除を行います。

    ```
    dism /unmount-wim /mountdir:c:\mountRestore /commit
    ```

8.  [RestoreMediaroot]\Sources\Boot_x86.wim に対して手順 2 ～ 7 を繰り返します。

9. 次の手順を実行して、イメージのコミットとマウント解除を行います。

    ```
    dism /unmount-wim /mountdir:c:\mount /commit
    ```

## <a name="see-also"></a>参照

 [イメージの作成とカスタマイズ追加の](Creating-and-Customizing-the-Image.md)[カスタマイズ](Additional-Customizations.md)[展開のイメージの準備](Preparing-the-Image-for-Deployment.md)[カスタマーエクスペリエンスのテスト](Testing-the-Customer-Experience.md)