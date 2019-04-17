---
title: Active Directory ドメインに NPS サーバーを登録します。
description: このトピックを使用すると、または別のドメインに NPS サーバーの既定のドメインでの Windows Server 2016 でネットワーク ポリシー サーバーを実行しているサーバーを登録します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2de954fd-a7d8-4cc6-85b1-b0c3c06f788f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7ba18f6c994e8b15da3a07a3e37550d5dbff24af
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="register-an-nps-server-in-an-active-directory-domain"></a>Active Directory ドメインに NPS サーバーを登録します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、または別のドメインに NPS サーバーの既定のドメインでの Windows Server 2016 でネットワーク ポリシー サーバーを実行しているサーバーを登録します。

## <a name="register-an-nps-server-in-its-default-domain"></a>既定のドメインに NPS サーバーを登録します。

この手順を使用するには、サーバーがドメインのメンバーがドメインに NPS サーバーを登録します。 

NPS サーバーは、承認プロセス中にユーザー アカウントのダイヤルイン プロパティを読み取るアクセス許可があるために、Active Directory に登録する必要があります。 サーバーを追加する NPS サーバーの登録、**RAS および IAS サーバー** Active Directory にグループ化します。

メンバーシップ**管理者**、またはそれと同等がこれらの手順を実行するために必要な最小値。

### <a name="to-register-an-nps-server-in-its-default-domain"></a>既定のドメインに NPS サーバーを登録するには


1. NPS サーバーで、サーバー マネージャーで、をクリックして**ツール**、] をクリックし、**ネットワーク ポリシー サーバー**します。 ネットワーク ポリシー サーバー コンソールが開きます。

2. 右クリック**NPS (ローカル)**、] をクリックし、**Active Directory でサーバーの登録**します。 **ネットワーク ポリシー サーバー** ] ダイアログ ボックスが開きます。

3. **ネットワーク ポリシー サーバー**、] をクリックして**OK**、] をクリックし、**[OK]**もう一度します。

## <a name="register-an-nps-server-in-another-domain"></a>別のドメインに NPS サーバーを登録します。

Active Directory 内のユーザー アカウントのダイヤルイン プロパティを読み取るアクセス許可を持つ NPS サーバーを提供するには、アカウントが存在するドメインに NPS サーバーを登録する必要があります。

この手順を使用すると、NPS サーバーがドメイン メンバーではないドメインに NPS サーバーを登録します。

メンバーシップ**管理者**、またはそれと同等がこれらの手順を実行するために必要な最小値。

### <a name="to-register-an-nps-server-in-another-domain"></a>別のドメインに NPS サーバーを登録するには

1. ドメイン コントローラー、サーバー マネージャーで、クリックして**ツール**、] をクリックし、**Active Directory ユーザーとコンピューター**します。 Active Directory ユーザーとコンピューター コンソールが開きます。

2. コンソール ツリーで、ユーザー アカウントの情報を読み取る NPS サーバーのドメインに移動し、**ユーザー**フォルダー。 

3. 詳細ウィンドウで右クリックして**RAS および IAS サーバー**、] をクリックし、**プロパティ**します。 **RAS および IAS サーバーのプロパティ**] ダイアログ ボックスが開きます。

4. **RAS および IAS サーバーのプロパティ**ダイアログ ボックスで、] をクリックして、**メンバー** ] タブで、各ドメインで、登録し、をクリックする NPS サーバーの追加**OK**します。


### <a name="to-register-an-nps-server-in-another-domain-by-using-netsh-commands-for-nps"></a>NPS の Netsh コマンドに関するページを使用して、別のドメインに NPS サーバーを登録するには

1. コマンド プロンプトまたは windows PowerShell を開きます。 

2. コマンド プロンプトで、次を入力します。**netsh nps 追加 registeredserver**&nbsp;*ドメイン*&nbsp;*サーバー*、し、Enter キーを押します。

>[!NOTE]
>上記のコマンドでは、*ドメイン*は、NPS サーバーを登録するドメインの DNS ドメイン名と*サーバー* NPS サーバーのコンピューターの名前です。

