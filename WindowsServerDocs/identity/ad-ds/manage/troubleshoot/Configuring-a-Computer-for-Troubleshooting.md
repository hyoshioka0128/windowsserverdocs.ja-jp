---
ms.assetid: 155abe09-6360-4913-8dd9-7392d71ea4e6
title: トラブルシューティング用コンピューターを構成する
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1acb5f7d309d58ed4a5a3aca6bb89f01c0cbf933
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854123"
---
# <a name="configuring-a-computer-for-troubleshooting"></a>トラブルシューティング用コンピューターを構成する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

特定し、Active Directory の問題を修正する高度なトラブルシューティングの手法を使用する前に、トラブルシューティングのためにコンピューターを構成します。 トラブルシューティングの概念、手順、およびツールの基本的な知識も必要です。

Windows Server の監視ツールの詳細については、ステップ バイ ステップ ガイドを参照してください[パフォーマンスと信頼性の Windows Server の監視。](https://go.microsoft.com/fwlink/?LinkId=123737)

## <a name="configuration-tasks-for-troubleshooting"></a>トラブルシューティングのための構成タスク

Active Directory Domain Services (AD DS) のトラブルシューティングには、コンピューターを構成するには、次のタスクを実行します。

### <a name="install-remote-server-administration-tools-for-ad-ds"></a>AD DS 用のリモート サーバー管理ツールをインストールします。

ドメイン コント ローラーを作成する AD DS をインストールするときに、AD DS の管理に使用する管理ツールが自動的にインストールされます。 ドメイン コント ローラーをドメイン コント ローラーではないコンピューターからリモートで管理する場合は、メンバー サーバーまたは Windows のサポートされているバージョンを実行しているワークステーションでリモート サーバー管理ツール (RSAT) をインストールできます。 RSAT には、Windows Server 2003 から Windows サポート ツールが置き換えられます。

RSAT をインストールする方法の詳細については、この記事を参照してください。[リモート サーバー管理ツール](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)します。

### <a name="configure-reliability-and-performance-monitor"></a>信頼性およびパフォーマンス モニターを構成します。

Windows Server は、Windows 信頼性およびパフォーマンス モニターは、パフォーマンス ログと警告、Server Performance Advisor などの以前のスタンドアロン ツールの機能を結合する Microsoft 管理コンソール (MMC) スナップインが含まれています。システム モニターを選択します。 このスナップインには、データ コレクター セットおよびイベント トレース セッションをカスタマイズするため、グラフィカル ユーザー インターフェイス (GUI) を提供します。

信頼性およびパフォーマンス モニターは、信頼性モニター、システムに対する変更を追跡し、システム安定性の変更と比較した MMC スナップインの関係のグラフィカル ビューを提供することをも含まれます。

### <a name="set-logging-levels"></a>ログ記録レベルを設定します。

イベント ビューアーで、ディレクトリ サービス ログで受信した情報がトラブルシューティングのために十分ではない場合に適切なレジストリ エントリを使用して、ログ記録レベルを上げる**HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics**します。

既定では、すべてのエントリのログ記録レベルに設定**0**最小限の情報を提供します。 最上位のログ記録レベルは**5**します。 エントリのレベルを広げると、ディレクトリ サービス イベント ログに記録されるイベントを追加します。

診断エントリのログ記録レベルを変更するのにには、次の手順を使用します。 この手順を完了するには、少なくとも **Domain Admins** グループ、またはそれと同等のメンバーシップが必要です。

> [!WARNING]
> 他の手段がない限り、レジストリは直接編集しないことをお勧めします。 レジストリに対する変更は検証されません、レジストリ エディターで、または Windows によって前に、それらを適用し、結果として、不適切な値を格納することができます。 回復不能なエラーは、システムで、これがあります。 可能であれば、レジストリを直接編集するのではなく、タスクを実行するのにグループ ポリシーまたは MMC スナップインなどの他の Windows ツールを使用します。 レジストリを編集する必要がある場合は、細心の注意が必要です。
>

診断エントリのログ記録レベルを変更するには

1. をクリックして**開始** > **実行**> 型**regedit** > をクリックして**OK**します。
2. ログ記録を設定するエントリに移動します。
   * 例:HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics
3. エントリをダブルクリックし、[**ベース**、] をクリックして**Decimal**。
4. **値**から整数を入力**0**を通じて**5**、順にクリックします**OK**します。
