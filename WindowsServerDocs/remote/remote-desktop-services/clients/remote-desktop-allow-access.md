---
title: リモート デスクトップ - PC へのアクセスを許可する
description: PC にリモートからアクセスするためのオプションについて
ms.topic: article
ms.assetid: 0f1557ed-53f7-4333-b023-c8e0f4b58bf4
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f581aeee099c906c970fdc320150fd1d6c102e17
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946525"
---
# <a name="remote-desktop---allow-access-to-your-pc"></a>リモート デスクトップ - PC へのアクセスを許可する

>適用先:Windows 10、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

リモート デスクトップを使用して接続し、[Microsoft リモート デスクトップ クライアント](remote-desktop-clients.md) (Windows、iOS、macOS、Android 向けに提供) を使用してリモート デバイスから PC を制御することができます。 PC へのリモート接続を許可すると、別のデバイスを使用して PC に接続し、自分のデスクで作業しているかのように、すべてのアプリ、ファイル、ネットワーク リソースにアクセスすることができます。

> [!NOTE]
> リモート デスクトップを使用して、Windows 10 Pro/Enterprise、Windows 8.1/8 Enterprise/Pro、Windows 7 Professional/Enterprise/Ultimate、および Windows Server の Windows Server 2008 よりも新しいバージョンに接続できます。 (Windows 10 Home のような) Home エディションを実行しているコンピューターには接続できません。

リモート PC に接続するには、そのコンピューターがオンになっていて、そこにネットワーク接続が備わっており、リモート デスクトップが有効になっている必要があります。また、リモート コンピューターへのネットワーク アクセスが可能 (これはインターネット経由でもかまいません) で、接続のためのアクセス許可を持っている必要があります。 接続のためのアクセス許可については、ユーザーの一覧に含まれている必要があります。 接続を開始する前に、接続先コンピューターの名前を調べ、そのコンピューターのファイアウォールを通したリモート デスクトップ接続が許可されていることを確認するのは良い考えです。

## <a name="how-to-enable-remote-desktop"></a>リモート デスクトップを有効にする方法

リモート デバイスから PC へのアクセスを許可する最も簡単な方法は、[設定] の下にあるリモート デスクトップのオプションを使用することです。 この機能は Windows 10 Fall Creators update (1709) で追加されたため、以前のバージョンの Windows に向けて、同様の機能を提供するダウンロード可能な別個のアプリが提供されています。 リモート デスクトップを有効にする従来の方法を使用することもできます。ただし、この方法で提供される機能と検証はより限定されたものになります。

### <a name="windows-10-fall-creator-update-1709-or-later"></a>Windows 10 Fall Creator Update (1709) 以降

いくつかの簡単なステップで PC のリモート アクセスを構成できます。
1. 接続先のデバイス上で **[スタート]** を選択し、左側の **[設定]** アイコンをクリックします。
2. **[システム]** グループを選択し、続いて [ **[リモート デスクトップ]** ](ms-settings:remotedesktop) 項目を選択します。
3. スライダーを使用してリモート デスクトップを有効にします。
4. また、接続が容易になるように、PC を起動状態かつ発見可能に保つことをお勧めします。 **[設定の表示]** をクリックして有効にします。
5. 必要に応じて、 **[この PC にリモートでアクセスできるユーザーの選択]** をクリックし、リモートで接続できるユーザーを追加します。
   1. Administrators グループのメンバーにはアクセス権が自動的に与えられます。
6. **[How to connect to this PC]** (この PC への接続方法) の下にあるこの PC の名前を書き留めます。 クライアントを構成するときに、これが必要になります。

### <a name="windows-7-and-early-version-of-windows-10"></a>Windows 7 および初期のバージョンの Windows 10

PC のリモート アクセスを構成するには、[Microsoft リモート デスクトップ アシスタント](https://www.microsoft.com/download/details.aspx?id=50042)をダウンロードして実行します。 このアシスタントは、リモート アクセスが有効になるようにシステム設定を更新し、コンピューターが接続のために起動状態になるようにして、ファイアウォールでリモート デスクトップ接続が許可されていることを確認します。

### <a name="all-versions-of-windows-legacy-method"></a>すべてのバージョンの Windows (従来の方法)

レガシ システムのプロパティを使用してリモート デスクトップを有効にするには、「[リモート デスクトップ接続を使用して別のコンピューターに接続する](https://windows.microsoft.com/windows/remote-desktop-connection-faq)」の指示に従います。

## <a name="should-i-enable-remote-desktop"></a>リモート デスクトップを有効にする必要があるか

PC を物理的に使用しているときにアクセスするだけであれば、リモート デスクトップを有効にする必要はありません。 リモート デスクトップを有効にすると、ローカル ネットワークから見えている PC 上のポートが開かれます。 リモート デスクトップを有効にするのは、自宅などの信頼できるネットワーク内のみにする必要があります。 また、アクセスが厳密に制御されているような PC では、リモート デスクトップを有効にしないことをお勧めします。

リモート デスクトップへのアクセスを有効にすると、Administrators グループに属する全員と、選択した追加のユーザーすべてに、コンピューター上の彼らのアカウントにリモートからアクセスする機能を付与していることに注意してください。

PC にアクセスできるすべてのアカウントが、強力なパスワードを使用して構成されているようにする必要があります。

## <a name="why-allow-connections-only-with-network-level-authentication"></a>ネットワーク レベル認証でのみ接続を許可する理由

PC にアクセスできるユーザーを制限する場合は、ネットワーク レベル認証 (NLA) でのみアクセスを許可することを選択します。 このオプションを有効にすると、ユーザーは PC に接続する前に、ネットワークに対して自分自身を認証する必要があります。 NLA を使用してリモート デスクトップを実行しているコンピューターからの接続のみを許可することは、悪意のあるユーザーやソフトウェアからコンピューターを保護することに役立つ、より安全な認証方法です。 NLA とリモート デスクトップの詳細については、[RDS 接続のための NLA の構成](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732713(v=ws.11))に関するページを参照してください。

自宅ネットワーク上の PC に、そのネットワークの外部からリモート接続しようとしている場合は、このオプションを選択しないでください。
