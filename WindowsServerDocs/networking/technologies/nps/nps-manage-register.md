---
title: Active Directory ドメインに NPS を登録する
description: このトピックでは、NPS の既定のドメインまたは別のドメイン内の Windows Server 2016 でネットワーク ポリシー サーバーを実行しているサーバーの登録を使用できます。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2de954fd-a7d8-4cc6-85b1-b0c3c06f788f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4a289ec519e5107576becf2905cd881cf9def190
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877653"
---
# <a name="register-an-nps-in-an-active-directory-domain"></a>Active Directory ドメインに NPS を登録する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、NPS の既定のドメインまたは別のドメイン内の Windows Server 2016 でネットワーク ポリシー サーバーを実行しているサーバーの登録を使用できます。

## <a name="register-an-nps-in-its-default-domain"></a>既定のドメインに NPS を登録します。

この手順を使用するには、サーバーがドメイン メンバーでは、ドメインに NPS を登録します。 

NPSs は、承認プロセス中にユーザー アカウントのダイヤルイン プロパティを読み取るアクセス許可があるために、Active Directory に登録する必要があります。 サーバーを追加、NPS の登録、 **RAS and IAS Servers** Active Directory でグループ化します。

これらの手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

### <a name="to-register-an-nps-in-its-default-domain"></a>既定のドメインに NPS を登録するには


1. NPS では、サーバー マネージャーで、をクリックして**ツール**、 をクリックし、**ネットワーク ポリシー サーバー**します。 ネットワーク ポリシー サーバー コンソールが開きます。

2. 右クリック**NPS (ローカル)**、 をクリックし、 **Active Directory でサーバーの登録**します。 **[ネットワーク ポリシー サーバー]** ダイアログ ボックスが開きます。

3. **[ネットワーク ポリシー サーバー]** の **[OK]** をクリックし、もう一度 **[OK]** をクリックします。

## <a name="register-an-nps-in-another-domain"></a>NPS を別のドメインを登録します。

Active Directory 内のユーザー アカウントのダイヤルイン プロパティを読み取るアクセス許可を持つ、NPS を提供するには、アカウントが存在するドメインに NPS を登録する必要があります。

この手順を使用すると、NPS がドメイン メンバーではないドメインに NPS を登録します。

これらの手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

### <a name="to-register-an-nps-in-another-domain"></a>別のドメインに NPS を登録するには

1. ドメイン コント ローラーで、サーバー マネージャーで、次のようにクリックします。**ツール**、 をクリックし、 **Active Directory ユーザーとコンピューター**します。 Active Directory ユーザーとコンピューター コンソールが開きます。

2. コンソール ツリーでユーザー アカウントの情報を読み取る NPS ドメインに移動し、順にクリックして、**ユーザー**フォルダー。 

3. 詳細ペインで右クリックして**RAS and IAS Servers**、 をクリックし、**プロパティ**します。 **RAS および IAS サーバーのプロパティ** ダイアログ ボックスが表示されます。

4. **RAS および IAS サーバーのプロパティ**ダイアログ ボックスで、をクリックして、**メンバー**  タブで、クリックして、ドメインに登録したい NPSs の各追加**OK**。


### <a name="to-register-an-nps-in-another-domain-by-using-netsh-commands-for-nps"></a>NPS の Netsh コマンドを使用して、別のドメインに NPS を登録するには

1. コマンド プロンプトまたは windows PowerShell を開きます。 

2. コマンド プロンプトで、次の入力: **netsh nps 追加 registeredserver** &nbsp;*ドメイン* &nbsp; *server*、し、ENTER キーを押します。

>[!NOTE]
>上記のコマンドでは、*ドメイン*は、NPS を登録するドメインの DNS ドメイン名と*サーバー* NPS コンピューターの名前を指定します。

