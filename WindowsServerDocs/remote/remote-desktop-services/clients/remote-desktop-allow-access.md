---
title: リモート デスクトップ - お使いの PC へのアクセスを許可します。
description: お使いの PC へのリモート アクセスするためのオプションについて説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f1557ed-53f7-4333-b023-c8e0f4b58bf4
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: af41304e08f19ca155f6fd13c9258e9a8f20c163
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817013"
---
# <a name="remote-desktop---allow-access-to-your-pc"></a>リモート デスクトップ - お使いの PC へのアクセスを許可します。

>適用先:Windows 10、Windows 8.1、Windows Server 2012 R2、Windows Server 2016

リモート デスクトップを使用してに接続しを使用して、PC リモート デバイスからを制御することができます、 [Microsoft リモート デスクトップ クライアント](remote-desktop-clients.md)(Windows、iOS、macOS、Android の使用可能)。 お使いの PC にリモート接続を許可する場合は、お使いの PC に接続し、自分の席にすわって場合と同様に、アプリ、ファイル、およびネットワーク リソースのすべてにアクセス権を持つ別のデバイスを使用できます。  

> [!NOTE]
> Windows 10 Pro Enteprise、Windows 8.1、および 8 Enterprise、Pro、Windows 7 Professional、Enterprise、および Ultimate、および Windows Server のバージョン Windows Server 2008 よりも新しいへの接続には、リモート デスクトップを使用することができます。 (のように Windows 10 Home)、Home edition を実行しているコンピューターに接続することはできません。 

接続する権限が必要し、するコンピューターをオン、ネットワーク接続が必要、リモート デスクトップを有効にする必要がありますをリモート PC に接続する (インターネット経由でも)、リモート コンピューターへのネットワーク アクセスがあります。 接続するアクセス許可は、ユーザーの一覧である必要があります。 接続を開始する前にに接続しているコンピューターの名前を検索して、ファイアウォール経由のリモート デスクトップ接続が許可されているかどうかを確認することをお勧めです。

## <a name="how-to-enable-remote-desktop"></a>リモート デスクトップを有効にする方法

お使いの PC にリモート デバイスからのアクセスを許可する最も簡単な方法は、[設定] でリモート デスクトップのオプションを使用してください。 以前のバージョンの Windows 同様の機能を提供するため、この機能は個別のダウンロード可能な Windows 10 Fall Creators update (1709) で追加されたアプリも使用します。 このメソッドは、機能性と検証を提供します。 ただし、リモート デスクトップを有効にするは、従来の方法を使用することもできます。

### <a name="windows-10-fall-creator-update-1709-or-later"></a>Windows 10 Fall Creator Update (1709) またはそれ以降

いくつかの簡単なステップでは、PC のリモート アクセスを構成できます。
1. 接続するデバイスで、次のように選択します。**開始** をクリックし、**設定**左側のアイコン。
2. 選択、**システム**グループが続く、 [**リモート デスクトップ**](ms-settings:remotedesktop)項目。
3. スライダーを使用して、リモート デスクトップを有効にします。
4. また、起動状態と接続を容易に検出できるように、PC を保持することをお勧めします。 クリックして**設定を表示する**有効にします。
5. クリックしてリモートで接続できるユーザーを追加、必要に応じて**この PC をリモートでアクセスできるユーザーを選択します。** します。
   1. Administrators グループのメンバーは、アクセスを自動的にあります。
6. この PC の名前を書き留めて**この PC に接続する方法**します。 このクライアントを構成する必要があります。

### <a name="windows-7-and-early-version-of-windows-10"></a>Windows 7 および Windows 10 の初期のバージョン

リモート アクセスは、PC を構成するには、ダウンロードして実行、 [Microsoft リモート デスクトップ アシスタント](https://www.microsoft.com/download/details.aspx?id=50042)します。 このアシスタントは、リモート アクセスを有効にするシステム設定を更新、によりコンピューターが接続で起動され、ファイアウォールがリモート デスクトップ接続を許可することを確認します。 

### <a name="all-versions-of-windows-legacy-method"></a>すべてのバージョンの Windows (レガシ メソッド)

レガシ システムのプロパティを使用してリモート デスクトップを有効にする指示に従って、[リモート デスクトップ接続を使用して別のコンピューターへの接続](https://windows.microsoft.com/windows/remote-desktop-connection-faq)します。

## <a name="should-i-enable-remote-desktop"></a>リモート デスクトップを有効にする必要がありますか。

その前に物理的に座ってときに、PC にアクセスする場合は、リモート デスクトップを有効にする必要はありません。 リモート デスクトップを有効にするには、ローカル ネットワークに表示されている PC でのポートが表示されます。 自宅などの信頼されたネットワークでリモート デスクトップをのみ有効にする必要があります。 アクセスが厳密に制御されている任意の PC でのリモート デスクトップを有効にすることは避けたします。

有効にすると、リモート デスクトップへのアクセス、Administrators グループのすべてのユーザーを許可するときにその他のユーザーとを選択すること、リモート コンピューター上の自分のアカウントにアクセスすることに注意してください。

お使いの PC にアクセスできるすべてのアカウントが強力なパスワードで構成されていることを確認してください。

## <a name="why-allow-connections-only-with-network-level-authentication"></a>ネットワーク レベル認証でのみ接続を許可する理由 
 
お使いの PC にアクセスできるユーザーを制限する場合のみでネットワーク レベル認証 (NLA) のアクセスを許可する選択します。 このオプションを有効にすると、ユーザーは、PC に接続する前に、ネットワークに自身を認証する必要があります。 悪意のあるユーザーやソフトウェアからコンピューターを保護できるようにするより安全な認証方法は、NLA を使用してリモート デスクトップを実行しているコンピューターからのみ接続を許可します。 NLA とリモート デスクトップの詳細については、チェック アウト[RDS 接続の構成の NLA](https://technet.microsoft.com/library/cc732713(v=ws.11).aspx)します。 

そのネットワークの外部からホーム ネットワーク上の PC にリモートで接続している場合に、このオプションを選択しないでください。
