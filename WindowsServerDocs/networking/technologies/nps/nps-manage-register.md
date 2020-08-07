---
title: Active Directory ドメインに NPS を登録する
description: このトピックを使用して、Windows Server 2016 のネットワークポリシーサーバーを実行しているサーバーを NPS の既定のドメインまたは別のドメインに登録することができます。
manager: brianlic
ms.topic: article
ms.assetid: 2de954fd-a7d8-4cc6-85b1-b0c3c06f788f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 871e1f2563564e1c85287393cd4b587692a44db6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952149"
---
# <a name="register-an-nps-in-an-active-directory-domain"></a>Active Directory ドメインに NPS を登録する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、Windows Server 2016 のネットワークポリシーサーバーを実行しているサーバーを NPS の既定のドメインまたは別のドメインに登録することができます。

## <a name="register-an-nps-in-its-default-domain"></a>NPS を既定のドメインに登録する

この手順を使用して、サーバーがドメインメンバーとなっているドメインに NPS を登録できます。

NPSs は、承認プロセス中にユーザーアカウントのダイヤルインプロパティを読み取るアクセス許可を持つように Active Directory に登録する必要があります。 NPS を登録すると、Active Directory の**RAS AND IAS Servers**グループにサーバーが追加されます。

これらの手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

### <a name="to-register-an-nps-in-its-default-domain"></a>NPS を既定のドメインに登録するには


1. NPS の [サーバーマネージャーで、[**ツール**] をクリックし、[**ネットワークポリシーサーバー**] をクリックします。 ネットワークポリシーサーバーコンソールが開きます。

2. [ **NPS (ローカル)**] を右クリックし、[ **Active Directory でサーバーを登録**する] をクリックします。 **[ネットワーク ポリシー サーバー]** ダイアログ ボックスが開きます。

3. **[ネットワーク ポリシー サーバー]** の **[OK]** をクリックし、もう一度 **[OK]** をクリックします。

## <a name="register-an-nps-in-another-domain"></a>別のドメインに NPS を登録する

Active Directory のユーザーアカウントのダイヤルインプロパティを読み取るためのアクセス許可を NPS に付与するには、アカウントが存在するドメインに NPS が登録されている必要があります。

次の手順を使用して、nps がドメインメンバーでないドメインに NPS を登録できます。

これらの手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

### <a name="to-register-an-nps-in-another-domain"></a>NPS を別のドメインに登録するには

1. ドメインコントローラーの [サーバーマネージャーで、[**ツール**] をクリックし、[ **Active Directory ユーザーとコンピューター**] をクリックします。 Active Directory ユーザーとコンピューター] コンソールが開きます。

2. コンソールツリーで、NPS がユーザーアカウント情報を読み取るドメインに移動し、[ **Users** ] フォルダーをクリックします。

3. 詳細ウィンドウで、[ **RAS および IAS サーバー**] を右クリックし、[**プロパティ**] をクリックします。 [ **RAS および IAS サーバーのプロパティ**] ダイアログボックスが表示されます。

4. [ **RAS および IAS サーバーのプロパティ**] ダイアログボックスで、[**メンバー** ] タブをクリックし、ドメインに登録する各 npss を追加して、[ **OK**] をクリックします。


### <a name="to-register-an-nps-in-another-domain-by-using-netsh-commands-for-nps"></a>NPS の Netsh コマンドを使用して NPS を別のドメインに登録するには

1. コマンドプロンプトまたは windows PowerShell を開きます。

2. コマンドプロンプトで、「 **netsh nps add registeredserver** &nbsp; *domain* &nbsp; *server*」と入力し、enter キーを押します。

>[!NOTE]
>上記のコマンドでは、*ドメイン*は nps を登録するドメインの DNS ドメイン名であり、 *server*は nps コンピューターの名前です。

