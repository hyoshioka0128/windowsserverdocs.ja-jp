---
title: リモート デスクトップ サービス VDI でサポートされる Windows 10 のセキュリティ構成
description: Windows Server 2016 の RDS によって Windows 10 VDI でサポートされる構成に関する情報を提供します。
ms.author: elizapo
ms.date: 10/27/2016
ms.topic: article
ms.assetid: 8f164f5d-a498-4f91-a12f-3e01d554f810
author: lizap
manager: dongill
ms.openlocfilehash: 7fd8de56d02dfe83add67b740405265a232747d9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946345"
---
# <a name="supported-windows-10-security-configurations-for-remote-desktop-services-vdi"></a>リモート デスクトップ サービス VDI でサポートされる Windows 10 のセキュリティ構成

> 適用先:Windows Server 2016

Windows 10 と Windows Server 2016 には、オペレーティング システムに新しい保護層が組み込まれています。これにより、セキュリティ違反に対する防御を強化し、悪意ある攻撃のブロックに役立てて、仮想マシン、アプリケーション、およびデータのセキュリティを強化しています。

> [!NOTE]
> [リモート デスクトップ サービスでサポートされる構成情報](rds-supported-config.md)を必ず確認してください。

次の表は、RDS を使用する VDI の展開で、これらの新機能のどれがサポートされているかの概要を示しています。

|  VDI のコレクションの種類               |  管理対象のプール型 |  管理対象の個人用 |  非管理対象のプール型                                     |  非管理対象の個人用                                    |
|-------------------------------------|------------------|--------------------|--------------------------------------------------------|--------------------------------------------------------|
| [Credential Guard](/windows/security/identity-protection/credential-guard/credential-guard)                    | はい              | はい                | はい                                                    | はい                                                    |
| [Device Guard](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)                        | はい              | はい                | はい                                                    | はい                                                    |
| [Remote Credential Guard](/windows/security/identity-protection/remote-credential-guard)             | いいえ               | いいえ                 | いいえ                                                     | いいえ                                                     |
| [シールド型で暗号化がサポートされる VM](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) | いいえ               | いいえ                 | 追加の構成によって暗号化がサポートされる VM | 追加の構成によって暗号化がサポートされる VM |

## <a name="remote-credential-guard"></a>Remote Credential Guard:

Remote Credential Guard がサポートされるのは、ターゲット マシンへの直接接続に対してのみで、リモート デスクトップ接続ブローカーやリモート デスクトップ ゲートウェイを回する接続に対してはサポートされません。
> [!NOTE]
> 単一インスタンス環境内に接続ブローカーがあり、DNS 名がコンピューター名と一致している場合、サポートはされませんが、Remote Credential Guard を使用できる可能性があります。

## <a name="shielded-vms-and-encryption-supported-vms"></a>シールド型 VM と暗号化がサポートされる VM:

- リモート デスクトップ サービス VDI ではシールド型 VM はサポートされません

暗号化がサポートされる VM を活用するには:
- 非管理対象コレクションと、リモート デスクトップ サービスのコレクション作成プロセスの外部にあるプロビジョニング テクノロジを使用して仮想マシンをプロビジョニングします。
- ユーザー プロファイル ディスクは、差分ディスクに依存しているためサポートされません
