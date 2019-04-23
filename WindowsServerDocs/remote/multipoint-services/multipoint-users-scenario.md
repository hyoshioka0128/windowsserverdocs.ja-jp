---
title: MultiPoint Services ユーザー アカウント
description: MultiPoint Services では、特にさまざまなシナリオを使用する種類のユーザー アカウントについて説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f3c6ce5-9b7c-45a0-83c5-3f9b9f5f48d4
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 31279f81d5af597b0b1f1729c953fefaf24a214f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855363"
---
# <a name="example-scenarios-multipoint-services-user-accounts"></a>シナリオの例:MultiPoint Services ユーザー アカウント
MultiPoint サービス環境内に選択したユーザー アカウントのシナリオを実装するために必要なもの 次の表では、ユーザー アカウントを構成し、スタンドアロンの MultiPoint コンピューターまたはネットワークに接続されたサーバーをワークグループまたは Active Directory ドメイン上の共有または個々 のユーザー アカウントのステーションを準備するために実行するには、各タスクについて説明します。 お客様の環境に適用されるシナリオを選択します。 必要な構成タスクそれぞれを完了するテーブル内のリンクをたどります。  
  
> [!NOTE]  
> ユーザー アカウントを設定する方法を決定していない場合は、次を参照してください。 [MultiPoint サービス環境内のユーザー アカウントを計画](Plan-user-accounts-for-your-MultiPoint-services-environment.md)選択肢がユーザーに与える影響の詳細についてはします。  
  
## <a name="single-multipoint-services-computer-in-a-stand-alone-environment-no-network"></a>スタンドアロン環境 (ネットワーク) にある単一の MultiPoint サービス コンピューター  
  
|||  
|-|-|  
|**ユーザーがログオンする必要はありません。** ステーションはすべてのユーザーにそれらを使用することはできます。 データまたはパーソナライズされたデスクトップを格納するためのプライベート フォルダーが含まれる各 Windows デスクトップ エクスペリエンスは不要です。|1. 1 つのローカル ユーザー アカウントを作成する (手順については、次を参照してください[ローカル ユーザー アカウントを作成する](Create-local-user-accounts.md)。)。<br />2. [複数のセッションが 1 つのアカウントを許可します。](Allow-one-account-to-have-multiple-sessions.md)<br />3.[自動ログオン用ステーションを構成します。](Configure-stations-for-automatic-logon.md)|  
|**同じユーザーのログオン ユーザーをできますすべて共有。** データまたはパーソナライズされたデスクトップを格納するためのプライベート フォルダーが含まれる各 Windows デスクトップ エクスペリエンスは不要です。|1. 1 つのローカル ユーザー アカウントを作成する (手順については、次を参照してください[ローカル ユーザー アカウントを作成する](Create-local-user-accounts.md)。)。<br />2. [複数のセッションが 1 つのアカウントを許可します。](Allow-one-account-to-have-multiple-sessions.md)|  
|**ユーザーが独自個々 の Windows デスクトップ エクスペリエンスが必要です。**|各ユーザーのローカル ユーザー アカウントを作成する (手順については、次を参照してください[ローカル ユーザー アカウントを作成する](Create-local-user-accounts.md)。)。|  
  
## <a name="multiple-multipoint-services-computers-on-a-network-but-with-no-domain"></a>複数の MultiPoint Services コンピューターがネットワークでは、ドメインがありません。  
  
|||  
|-|-|  
|**ユーザーがログオンする必要はありません。** ステーションはすべてのユーザーにそれらを使用することはできます。 データまたはパーソナライズされたデスクトップを格納するためのプライベート フォルダーが含まれる各 Windows デスクトップ エクスペリエンスは不要です。|1. 各サーバーで単一のローカル ユーザー アカウントを作成します。 (手順については、次を参照してください[ローカル ユーザー アカウントを作成する](Create-local-user-accounts.md)。)。<br />2. [複数のセッションが 1 つのアカウントを許可する](Allow-one-account-to-have-multiple-sessions.md)各サーバーで<br />3.[自動ログオン用ステーションを構成する](Configure-stations-for-automatic-logon.md)各サーバーで|  
|**同じユーザーのログオン ユーザーをできますすべて共有。** データまたはパーソナライズされたデスクトップを格納するためのプライベート フォルダーが含まれる各 Windows デスクトップ エクスペリエンスは不要です。|1. 各サーバーで単一のローカル ユーザー アカウントを作成します。 (手順については、次を参照してください[ローカル ユーザー アカウントを作成する](Create-local-user-accounts.md)。)。<br />2. [複数のセッションが 1 つのアカウントを許可する](Allow-one-account-to-have-multiple-sessions.md)各サーバーにします。|  
|**ユーザーが独自個々 の Windows デスクトップ エクスペリエンスが必要です。**<br /><br />-   **オプション A** -ユーザーは常に同じ MultiPoint Services コンピューターに接続されているローカルのステーションを使用します。<br />-   **オプション B** -ユーザーは 1 つ以上の MultiPoint Services コンピューターのローカル ステーションを使用します。<br />-   **オプション C** -ユーザーは LAN 上のリモート クライアントを使用します。|-   **オプション A** -そのサーバーのユーザーは各サーバーで単一のローカル ユーザー アカウントを作成します。 (手順については、次を参照してください[ローカル ユーザー アカウントを作成する](Create-local-user-accounts.md)。)。<br />-   **オプション B** -すべてのサーバーですべてのユーザーのローカル ユーザー アカウントを作成します。 **注:** これは、各ユーザーが各サーバーで、プロファイルを持つことを意味します。 つまり、サーバー A のステーションにログオンしているときに、マイ ドキュメント ファイルを保存する場合は表示されません、ファイル サーバー B のステーションにログオンするとき。 (手順については、次を参照してください[ローカル ユーザー アカウントを作成する](Create-local-user-accounts.md)。)。<br />-   **オプション C** -特定の MultiPoint Services コンピューターに各ユーザーを割り当てます。 各サーバーで、割り当てられたユーザーのローカル ユーザー アカウントを作成します。 (手順については、次を参照してください[ローカル ユーザー アカウントを作成する](Create-local-user-accounts.md)。)。|  
  
## <a name="one-or-more-multipoint-services-computers-in-a-domain-network-environment"></a>ドメイン ネットワーク環境で 1 つまたは複数の MultiPoint サービス コンピューター  
  
|||  
|-|-|  
|**ユーザーがログオンする必要はありません。** ステーションはすべてのユーザーにそれらを使用することはできます。 データまたはパーソナライズされたデスクトップを格納するためのプライベート フォルダーが含まれる各 Windows デスクトップ エクスペリエンスは不要です。|1. サーバーにログオンするためのドメイン アカウントを作成します。<br />2. [複数のセッションが 1 つのアカウントを許可する](Allow-one-account-to-have-multiple-sessions.md)各サーバーにします。<br />3.[自動ログオン用ステーションを構成する](Configure-stations-for-automatic-logon.md)各サーバーにします。|  
|**同じユーザーのログオン ユーザーをできますすべて共有。** データまたはパーソナライズされたデスクトップを格納するためのプライベート フォルダーが含まれる各 Windows デスクトップ エクスペリエンスは不要です。|1. グループまたはユーザーごとに、ドメイン アカウントを作成します。<br />2. [複数のセッションが 1 つのアカウントを許可する](Allow-one-account-to-have-multiple-sessions.md)各サーバーにします。|  
|**ユーザーが独自個々 の Windows デスクトップ エクスペリエンスが必要です。**<br /><br />-   **オプション A** -ドメイン アカウントを持つすべてのユーザーが MultiPoint Services コンピューターを使用できます。<br />-   **オプション B** -サーバーにアクセスできるドメイン アカウントを制限します。|-   **オプション A** -セットアップは不要です。 既定では、すべてのドメイン ユーザーは、MultiPoint Services コンピューターへのアクセスをネットワーク上にあります。<br />-   **オプション B** -MultiPoint Services コンピューターにドメイン ユーザー アカウントのアクセスを制限します。 手順については、次を参照してください。[サーバーへのユーザー アクセスを制限する](limit-users--access-to-the-server-in-multipoint-services.md)します。|  
|**ローカル ユーザー アカウントを使用して、ドメイン アカウントからそれらを個別に管理します。** たとえば、他のユーザーが MultiPoint Services がドメインではなく、管理するまたはドメイン アカウントを MultiPoint Services のすべてのユーザーに付与したくないです。|各サーバーでは、1 つまたは複数のローカル ユーザー アカウントを作成します。 (手順については、次を参照してください[ローカル ユーザー アカウントを作成する](Create-local-user-accounts.md)。)。<br /><br />**注:** これは、各ユーザー アカウントがあるプロファイルを各サーバーでことを意味します。 つまり、サーバー A のステーションにログオンしているときに、マイ ドキュメント ファイルを保存する場合は表示されません、ファイル サーバー B のステーションにログオンするとき。|  