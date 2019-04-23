---
title: Azure Site Recovery を使用して RDS のディザスター リカバリーを有効にします。
description: Azure Site Recovery を使用して RDS のディザスター リカバリーを有効にする方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 05/05/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: e3f9db4afb37452b4fd5d0229b385492b915fe45
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859013"
---
# <a name="enable-disaster-recovery-of-rds-using-azure-site-recovery"></a>Azure Site Recovery を使用して RDS のディザスター リカバリーを有効にします。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

ディザスター リカバリーのため、RDS デプロイが適切に構成されていることを確認するには、RDS デプロイを構成するコンポーネントのすべてを保護する必要があります。

- Active Directory
- SQL Server 層
- RDS のコンポーネント
- ネットワーク コンポーネント
 
## <a name="configure-active-directory-and-dns-replication"></a>Active Directory と DNS のレプリケーションを構成します。

作業を RDS デプロイのディザスター リカバリー サイトで Active Directory をする必要があります。 RDS デプロイに、どの程度複雑に基づく 2 つの選択肢があります。

- オプション 1 - アプリケーションの数が少ないがあり、1 つのドメイン コント ローラーにして、オンプレミス サイト全体は、サイト全体をまとめて、フェールオーバーして、使用して、ASR レプリケーション セカンダリ サイトの両方 (true に、ドメイン コント ローラーをレプリケートする場合サイト対サイトおよびサイトと Azure のシナリオ)。
- オプション 2 - 多数のアプリケーションがあると、Active Directory フォレストを実行しているし、フェールオーバー少数のアプリケーション、時に、ディザスター リカバリー サイトで、追加のドメイン コント ローラーをセットアップする場合 (どちらかセカンダリ サイトまたは Azure)。

参照してください[Protect Active Directory と DNS を Azure Site Recovery](/azure/site-recovery/site-recovery-active-directory)については、ディザスター リカバリー サイトでドメイン コント ローラーを使用できるようにします。 このガイドの残りの部分、これらの手順に従っているし、使用可能なドメイン コント ローラーがあることを仮定します。

## <a name="set-up-sql-server-replication"></a>SQL Server レプリケーションを設定します。

参照してください[SQL Server ディザスター リカバリーおよび Azure Site Recovery を使用して保護する SQL Server](/azure/site-recovery/site-recovery-sql) SQL Server レプリケーションをセットアップする手順についてはします。

## <a name="enable-protection-for-the-rds-application-components"></a>RDS アプリケーション コンポーネントの保護を有効にします。

RDS 展開の種類に応じて、異なるコンポーネント Vm (次の表に記載) されている Azure Site Recovery での保護を有効にできます。 HYPER-V または VMWare 上の Vm をデプロイするかどうかに基づいて、Azure Site Recovery の関連要素を構成します。

| 展開の種類                              | 保護の手順                                                                                                                                                                                      |
|----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 個人用の仮想デスクトップ (管理対象外)         |  1. すべての仮想化ホストが整いました RDVH 役割がインストールされたことを確認します。    </br>2. 接続ブローカーです。  </br>3.個人用デスクトップ。 </br>4。ゴールド テンプレート VM です。 </br>5。Web アクセス、ライセンス サーバー、およびゲートウェイ サーバー |
| プールされた仮想デスクトップが (UPD なしで管理) |  1. RDVH 役割がインストールされたすべての仮想化ホストが整いました。  </br>2. 接続ブローカーです。  </br>3.ゴールド テンプレート VM です。 </br>4。Web アクセス、ライセンス サーバー、およびゲートウェイ サーバー。                                  |
| Remoteapp とデスクトップ セッション (UPD なし)     |  1. セッション ホスト。  </br>2. 接続ブローカーです。 </br>3.Web アクセス、ライセンス サーバー、およびゲートウェイ サーバー。                                                                                                          |                                                                                                                                      |

