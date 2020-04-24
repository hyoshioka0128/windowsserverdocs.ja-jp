---
title: Azure Site Recovery を使用して RDS のディザスター リカバリーを有効にする
description: Azure Site Recovery を使用して RDS のディザスター リカバリーを有効にする方法について説明します。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 05/05/2017
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 0c7af18be4aa767009f1dd0b82f145ffe6874768
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80861405"
---
# <a name="enable-disaster-recovery-of-rds-using-azure-site-recovery"></a>Azure Site Recovery を使用して RDS のディザスター リカバリーを有効にする

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

ディザスター リカバリーに向けて RDS の展開が適切に構成されているようにするには、RDS の展開を構成しているすべてのコンポーネントを保護する必要があります。

- Active Directory
- SQL Server 階層
- RDS コンポーネント
- ネットワーク コンポーネント

## <a name="configure-active-directory-and-dns-replication"></a>Active Directory と DNS レプリケーションを構成する

RDS の展開が機能するためには、ディザスター リカバリー サイト上に Active Directory が必要です。 RDS の展開がどれほど複雑であるかに基づいて、2 つの選択肢があります。

- オプション 1 - オンプレミス サイト全体で、利用しているアプリケーションの数が少なく、ドメイン コント ローラーが 1 つであり、サイト全体を一緒にフェールオーバーする場合は、ASR レプリケーションを使用してドメイン コントローラーをセカンダリ サイトにレプリケートします (サイト間のシナリオとサイトから Azure へのシナリオの両方に該当)。
- オプション 2 - 多数のアプリケーションを利用していて、Active Directory フォレストを実行しており、同時にフェールオーバーするアプリケーションは少数である場合は、ディザスター リカバリー サイト (セカンダリ サイトまたは Azure 内のいずれか) に追加のドメイン コントローラーをセットアップします。

ディザスター リカバリー サイトでドメイン コントローラーを使用できるようにすることの詳細については、[Active Directory と DNS を Azure Site Recovery で保護すること](/azure/site-recovery/site-recovery-active-directory)に関するページを参照してください。 このガイドの残りの部分は、ユーザーがそれらの手順に従っており、使用可能なドメイン コントローラーがあることを前提としています。

## <a name="set-up-sql-server-replication"></a>SQL Server レプリケーションをセットアップする

SQL Server レプリケーションをセットアップする手順については、[SQL Server ディザスター リカバリーおよび Azure Site Recovery を使用して SQL Server を保護すること](/azure/site-recovery/site-recovery-sql)に関するページを参照してください。

## <a name="enable-protection-for-the-rds-application-components"></a>RDS アプリケーション コンポーネントの保護を有効にする

RDS 展開の種類に応じて、Azure Site Recovery で、異なるコンポーネントの VM の保護を (下の表に一覧を示すように) 有効にできます。 VM が Hyper-V または VMWare のどちらにデプロイされているかに基づいて、Azure Site Recovery の関連要素を構成します。


|               展開の種類                |                                                                                                     保護の手順                                                                                                     |
|----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     個人用仮想デスクトップ (管理対象外)     | 1.RDVH の役割がインストールされて、すべての仮想化ホストの準備が整っていることを確認します。    </br>2.接続ブローカー。  </br>3.個人用デスクトップ。 </br>4.ゴールド テンプレート VM。 </br>5.Web アクセス、ライセンス サーバー、およびゲートウェイ サーバー |
| プールされた仮想デスクトップ (UPD なしで管理) |                    1.RDVH の役割がインストールされて、すべての仮想化ホストの準備が整っている。  </br>2.接続ブローカー。  </br>3.ゴールド テンプレート VM。 </br>4.Web アクセス、ライセンス サーバー、およびゲートウェイ サーバー。                    |
|   RemoteApp とデスクトップ セッション (UPD なし)   |                                                          1.セッション ホスト。  </br>2.接続ブローカー。 </br>3.Web アクセス、ライセンス サーバー、およびゲートウェイ サーバー。                                                           |

