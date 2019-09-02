---
title: リモート デスクトップ サービス VDI でサポートされる Windows 10 のセキュリティ構成
description: Windows Server 2016 の RDS によって Windows 10 VDI でサポートされる構成に関する情報を提供します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 10/27/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8f164f5d-a498-4f91-a12f-3e01d554f810
author: lizap
manager: dongill
ms.openlocfilehash: ff890150dcea30c425267dcaae9b1bdbc6d78b8c
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "63743396"
---
# <a name="supported-windows-10-security-configurations-for-remote-desktop-services-vdi"></a>リモート デスクトップ サービス VDI でサポートされる Windows 10 のセキュリティ構成

> 適用先:Windows Server 2016

Windows 10 と Windows Server 2016 には、オペレーティング システムに新しい保護層が組み込まれています。これにより、セキュリティ違反に対する防御を強化し、悪意ある攻撃のブロックに役立てて、仮想マシン、アプリケーション、およびデータのセキュリティを強化しています。

> [!NOTE]
> [リモート デスクトップ サービスでサポートされる構成情報](rds-supported-config.md)を必ず確認してください。

次の表は、RDS を使用する VDI の展開で、これらの新機能のどれがサポートされているかの概要を示しています。

|  VDI のコレクションの種類               |  管理対象のプール型 |  管理対象の個人用 |  非管理対象のプール型                                     |  非管理対象の個人用                                    |
|-------------------------------------|------------------|--------------------|--------------------------------------------------------|--------------------------------------------------------|
| [Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)                    | 〇              | 〇                | 〇                                                    | 〇                                                    |
| [Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)                        | 〇              | 〇                | 〇                                                    | 〇                                                    |
| [Remote Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard)             | X               | X                 | X                                                     | X                                                     |
| [シールド型で暗号化がサポートされる VM](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) | X               | X                 | 追加の構成によって暗号化がサポートされる VM | 追加の構成によって暗号化がサポートされる VM |

## <a name="remote-credential-guard"></a>Remote Credential Guard:

Remote Credential Guard がサポートされるのは、ターゲット マシンへの直接接続に対してのみで、リモート デスクトップ接続ブローカーやリモート デスクトップ ゲートウェイを回する接続に対してはサポートされません。
> [!NOTE]
> 単一インスタンス環境内に接続ブローカーがあり、DNS 名がコンピューター名と一致している場合、サポートはされませんが、Remote Credential Guard を使用できる可能性があります。

## <a name="shielded-vms-and-encryption-supported-vms"></a>シールド型 VM と暗号化がサポートされる VM: 

- リモート デスクトップ サービス VDI ではシールド型 VM はサポートされません 

暗号化がサポートされる VM を活用するには:
- 非管理対象コレクションと、リモート デスクトップ サービスのコレクション作成プロセスの外部にあるプロビジョニング テクノロジを使用して仮想マシンをプロビジョニングします。 
- ユーザー プロファイル ディスクは、差分ディスクに依存しているためサポートされません 

