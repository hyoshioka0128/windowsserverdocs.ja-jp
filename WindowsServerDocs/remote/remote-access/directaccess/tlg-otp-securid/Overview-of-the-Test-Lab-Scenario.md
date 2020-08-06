---
title: テストラボのシナリオ OTP 認証と RSA SecurID の概要
description: このトピックは、「テストラボガイド-OTP 認証を使用した DirectAccess のデモンストレーション」と「RSA SecurID for Windows Server 2016」に含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: ce584811-b209-48fe-ab2b-4c399bd0bd79
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4e6167d7a363b0f6396f6af48234764ecf531fc2
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769130"
---
# <a name="overview-of-the-test-lab-scenario-otp-authentication-and-rsa-securid"></a>テストラボのシナリオ OTP 認証と RSA SecurID の概要

>適用先:Windows Server (半期チャネル)、Windows Server 2016

リモートアクセスは、windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 オペレーティングシステムのサーバーの役割で、リモートユーザーが、ルーティングとリモートアクセスサービス (RRAS) を使用して、DirectAccess または仮想プライベートネットワーク (Vpn) を使用して内部ネットワークリソースに安全にアクセスできるようにします。 このガイドでは、「リモートアクセスのワンタイムパスワード (OTP) 構成をデモンストレーションするための、 [IPv4 と IPv6 の混在を使用した DirectAccess シングルサーバーセットアップのデモンストレーション」の「テストラボガイド」](https://go.microsoft.com/fwlink/p/?LinkId=237004)を拡張する手順について説明します。

> [!WARNING]
> このテストラボガイドの設計には、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行するドメインコントローラー、証明機関 (CA) などのインフラストラクチャサーバーが含まれています。 このテストラボガイドを使用して、他のオペレーティングシステムを実行しているインフラストラクチャサーバーを構成することはできません。また、他のオペレーティングシステムを構成する手順については、このガイドでは説明しません。

## <a name="about-this-guide"></a>このガイドについて
Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 のリモートアクセスでは、OTP を使用したクライアント認証のサポートが追加されます。 このテストラボでは、リモートアクセスを使用した OTP 機能を示すために RSA SecurID のみを使用します。 その他の RADIUS ベースの OTP ソリューションもサポートされていますが、このテストラボの範囲外です。 このガイドでは、6 台のサーバーと 2 台のクライアント コンピューターを使うリモート アクセスを構成し、デモンストレーションを行う手順について説明します。 「OTP を使用したリモートアクセスの完了」テストラボでは、イントラネット、インターネット、ホームネットワークをシミュレートし、さまざまなインターネット接続シナリオでリモートアクセス機能を示します。

> [!IMPORTANT]
> このラボは、最小限のコンピューターを使って概念を実証するためのものです。 このガイドで詳しく説明されている構成は、テスト ラボでの使用のみを目的としています。運用環境では使用しないでください。



