---
title: Windows Server Essentials ADK の使用に関する重要な情報
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 26cb2992-1250-4672-98ee-8b870baa45d5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: fa1cee0d12182303a4c125089f11b121b848d6bf
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181218"
---
# <a name="important-information-for-using-the-windows-server-essentials-adk"></a>Windows Server Essentials ADK の使用に関する重要な情報

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials のイメージを作成してカスタマイズするには、 [windows 8 adk](https://go.microsoft.com/fwlink/?LinkId=248647)の多くのツールを使用しますが、WINDOWS 8 Adk と Windows SERVER essentials ADK にはいくつかの重要な違いがあります。

 次の重要な相違点に注意する必要があります。

-   **%windir%\setup\script\SetupComplete.cmd** の一部の設定が変更されています。 このコマンドを使用する場合、別のコマンド ラインを追加できますが、既存のコマンド ラインを削除することはできません。

## <a name="working-with-passwords"></a>パスワードの操作

-   管理者のパスワードがに設定され、 Admin@123 Install.wim\unattend.xml で自動ログオンが有効になります。 したがって、サーバーの初期構成中にパスワードを何度も入力する必要はありません。 リムーバブル メディアのルートにカスタマイズされた unattend.xml が存在する場合、この設定は上書きされるため、パスワードを設定し、スタートアップ中にログオンする必要があります。

-   初期構成中、エンド ユーザーは新しいアカウントとパスワードを作成するよう求められます。 この新しいアカウントが、オペレーティング システムのネットワーク管理者アカウントになります。 その後、管理者アカウントと自動ログオンは無効になります。 cfg.ini ファイルを使用すると、品質保証テスト用にこのプロセスを自動化できます。

-   unattend.xml ファイルの作成の詳細については、 [Windows 8 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) のドキュメントを参照してください。

## <a name="see-also"></a>参照

 [Windows Server ESSENTIALS ADK を使用したはじめに](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)[イメージの作成とカスタマイズ追加の](Creating-and-Customizing-the-Image.md)[カスタマイズカスタマイズ](Additional-Customizations.md)[のイメージの準備カスタマーエクスペリエンスをテストするためのイメージの準備](Preparing-the-Image-for-Deployment.md) [Testing the Customer Experience](Testing-the-Customer-Experience.md)

