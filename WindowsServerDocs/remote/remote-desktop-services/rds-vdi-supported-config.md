---
title: リモート デスクトップ サービスの VDI でサポートされる Windows 10 のセキュリティ構成
description: Windows Server 2016 で RDS での Windows 10 の VDI でサポートされる構成について説明します。
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820083"
---
# <a name="supported-windows-10-security-configurations-for-remote-desktop-services-vdi"></a>リモート デスクトップ サービスの VDI でサポートされる Windows 10 のセキュリティ構成

> 適用先:Windows Server 2016

Windows 10 および Windows Server 2016 をさらにセキュリティ侵害を防ぐため、悪意のある攻撃をブロックし、仮想マシン、アプリケーション、およびデータのセキュリティを強化、オペレーティング システムに組み込まれている保護の新しい層があります。

> [!NOTE]
> 必ず確認、[リモート デスクトップ サービスには、構成情報がサポートされている](rds-supported-config.md)します。

これらの新機能の rds. を使用して、VDI 展開でサポートされている次の表

|  VDI のコレクション型               |  プールの管理 |  個人の管理 |  プールされた非管理対象                                     |  非管理対象の個人                                    |
|-------------------------------------|------------------|--------------------|--------------------------------------------------------|--------------------------------------------------------|
| [Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)                    | 〇              | 〇                | 〇                                                    | 〇                                                    |
| [Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)                        | 〇              | 〇                | 〇                                                    | 〇                                                    |
| [Credential Guard をリモート](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard)             | X               | いいえ                 | いいえ                                                     | X                                                     |
| [シールドされた & 暗号化サポート Vm](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) | いいえ               | いいえ                 | 追加の構成でサポートされる Vm の暗号化 | 追加の構成でサポートされる Vm の暗号化 |

## <a name="remote-credential-guard"></a>Credential Guard をリモートの場合:

Credential Guard をリモートには、ターゲット コンピューターに直接接続していないのリモート デスクトップ接続ブローカーとリモート デスクトップ ゲートウェイ経由でのみサポートされます。
> [!NOTE]
> 接続ブローカー、単一インスタンス環境にある DNS 名がコンピューター名と一致する場合は、ことができます、リモートの Credential Guard を使用するが、これはサポートされていません。

## <a name="shielded-vms-and-encryption-supported-vms"></a>シールドされた Vm と暗号化には、Vm がサポートされています。 

- リモート デスクトップ サービスの VDI では、シールドされた Vm はサポートされていません 

サポートされる Vm の暗号化を活用するには。
- 非管理対象のコレクションと、リモート デスクトップ サービスのコレクションの作成プロセスの外部でプロビジョニングのテクノロジを使用して、仮想マシンをプロビジョニングします。 
- 差分ディスクに依存しているために、ユーザー プロファイル ディスクはサポートされていません 

