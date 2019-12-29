---
title: ファイルへのアクセスを高速にするため、Always Offline モードを有効にする
description: オフラインファイルの Always Offline モードを使用して、キャッシュされたファイルとリダイレクトされたフォルダーへのアクセスを高速化する方法について説明します。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 389fdd26a7e1d9824f1eaf0136a544547f08eb05
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401953"
---
# <a name="enable-always-offline-mode-for-faster-access-to-files"></a>ファイルへのアクセスを高速にするため、Always Offline モードを有効にする

>適用対象:Windows 10、windows 8、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012、Windows Server 2012 R2、および Windows (半期チャネル)

このドキュメントでは、オフラインファイルの Always Offline モードを使用して、キャッシュされたファイルとリダイレクトされたフォルダーにより高速にアクセスできるようにする方法について説明します。 また、ユーザーが高速ネットワーク接続を使用して接続されている場合でも、ユーザーは常にオフラインで作業しているため、always Offline では帯域幅の使用率が低くなります。

## <a name="prerequisites"></a>前提条件

Always Offline モードを有効にするには、環境が次の前提条件を満たしている必要があります。

- クライアントコンピューターがドメインに参加している Active Directory Domain Services (AD DS) ドメイン。 フォレストまたはドメインの機能レベルの要件やスキーマの要件はありません。
- Windows 10、Windows 8.1、Windows 8、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行するクライアントコンピューター。 (以前のバージョンの Windows を実行しているクライアントコンピューターは、高速ネットワーク接続では引き続きオンラインモードに移行する場合があります)。
- グループポリシー管理がインストールされているコンピューター。

## <a name="enable-always-offline-mode"></a>Always Offline モードを有効にする

Always Offline モードを有効にするには、グループポリシーを使用して [**低速リンクモードを構成**する] ポリシー設定を有効にし、待機時間を**1**ミリ秒に設定します。 これにより、Windows 8 または Windows Server 2012 を実行しているクライアントコンピューターは、Always Offline モードを自動的に使用します。

>[!NOTE]
>Windows 7、Windows Vista、Windows Server 2008 R2、または Windows Server 2008 を実行しているコンピューターは、ネットワーク接続の待機時間が1ミリ秒を下回ると、引き続きオンラインモードに移行する可能性があります。

1. **グループポリシー管理**を開きます。
2. 必要に応じてオフラインファイル設定の新しいグループポリシーオブジェクト (GPO) を作成するには、適切なドメインまたは組織単位 (OU) を右クリックし、[**このドメインに GPO を作成し、このコンテナーにリンク**する] を選択します。
3. コンソールツリーで、オフラインファイル設定を構成する GPO を右クリックし、 **[編集]** を選択します。 **グループポリシー管理エディター**が表示されます。
4. コンソールツリーの コンピューターの **[構成]** で、 **[ポリシー]** 、 **[管理用テンプレート]** 、 **[ネットワーク]** の順に展開し、 **[オフラインファイル]** を展開します。
5. **[低速リンクモードを構成する]** を右クリックし、 **[編集]** を選択します。 **[低速リンクモードの構成]** ウィンドウが表示されます。
6. **[有効]** を選びます。
7. **[オプション]** ボックスで、 **[表示]** を選択します。 [**内容の表示] ウィンドウ**が表示されます。
8. **[値の名前]** ボックスで、Always Offline モードを有効にするファイル共有を指定します。
9. すべてのファイル共有で Always Offline モードを有効にするには、 **\*** を入力します。
10. **[値]** ボックスに「 **latency = 1** 」と入力し、待機時間のしきい値を1ミリ秒に設定してから、[ **OK]** を選択します。

>[!NOTE]
>既定では、Always Offline モードの場合、Windows は、2時間ごとにバックグラウンドでオフラインファイルキャッシュ内のファイルを同期します。 この値を変更するには、 **[バックグラウンド同期の構成]** ポリシー設定を使用します。

## <a name="more-information"></a>詳細情報

* [フォルダーリダイレクト、オフラインファイル、移動ユーザープロファイルの概要](folder-redirection-rup-overview.md)
* [オフラインファイルでフォルダーリダイレクトを展開する](deploy-folder-redirection.md)