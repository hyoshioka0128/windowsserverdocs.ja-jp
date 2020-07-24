---
ms.assetid: 155abe09-6360-4913-8dd9-7392d71ea4e6
title: トラブルシューティング用コンピューターを構成する
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a71e1b92962ae9904262367f2c2697ecaa206ed8
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965934"
---
# <a name="configuring-a-computer-for-troubleshooting"></a>トラブルシューティング用コンピューターを構成する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

高度なトラブルシューティング手法を使用して Active Directory の問題を特定して修正する前に、トラブルシューティングのためにコンピューターを構成します。 また、トラブルシューティングの概念、手順、およびツールについての基本的な理解も必要です。

Windows Server 用の監視ツールの詳細については、 [Windows server のパフォーマンスと信頼性の監視](https://go.microsoft.com/fwlink/?LinkId=123737)に関するステップバイステップガイドを参照してください。

## <a name="configuration-tasks-for-troubleshooting"></a>トラブルシューティングの構成タスク

Active Directory Domain Services (AD DS) のトラブルシューティングのためにコンピューターを構成するには、次のタスクを実行します。

### <a name="install-remote-server-administration-tools-for-ad-ds"></a>AD DS のリモートサーバー管理ツールのインストール

AD DS をインストールしてドメインコントローラーを作成すると、AD DS の管理に使用する管理ツールが自動的にインストールされます。 ドメインコントローラーではないコンピューターからドメインコントローラーをリモートで管理する場合は、サポートされているバージョンの Windows を実行しているメンバーサーバーまたはワークステーションにリモートサーバー管理ツール (RSAT) をインストールすることができます。 RSAT は、windows サポートツールを Windows Server 2003 から置き換えます。

RSAT のインストールの詳細については、「[リモートサーバー管理ツール](../../../../remote/remote-server-administration-tools.md)」を参照してください。

### <a name="configure-reliability-and-performance-monitor"></a>信頼性とパフォーマンスモニターの構成

Windows Server には、Windows 信頼性とパフォーマンスモニターが含まれています。これは、パフォーマンスログと警告、サーバーパフォーマンスアドバイザー、システムモニターなど、以前のスタンドアロンツールの機能を組み合わせた Microsoft 管理コンソール (MMC) スナップインです。 このスナップインには、データコレクターセットおよびイベントトレースセッションをカスタマイズするためのグラフィカルユーザーインターフェイス (GUI) が用意されています。

信頼性とパフォーマンスモニターには、システムへの変更を追跡し、システムの安定性の変化と比較してそれらの関係をグラフィカルに表示する、信頼性モニターも含まれています。

### <a name="set-logging-levels"></a>ログ レベルの設定

イベントビューアーディレクトリサービスのログに記録された情報がトラブルシューティングに十分ではない場合は、 **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\ntds\diagnostics**で適切なレジストリエントリを使用してログレベルを上げます。

既定では、すべてのエントリのログ記録レベルは**0**に設定されます。これにより、最小限の情報が提供されます。 最も高いログ記録レベルは**5**です。 エントリのレベルを上げると、ディレクトリサービスのイベントログに追加のイベントが記録されます。

診断エントリのログ記録レベルを変更するには、次の手順に従います。 この手順を完了するには、少なくとも、**Domain Admins** グループ、またはそれと同等の権限を持つグループのメンバである必要があります。

> [!WARNING]
> 他の手段がない限り、レジストリは直接編集しないことをお勧めします。 レジストリの変更は、レジストリエディターまたは Windows によって適用される前には検証されず、その結果、間違った値が格納される可能性があります。 これにより、システムで回復不能なエラーが発生する可能性があります。 可能であれば、グループポリシーまたは MMC スナップインなどの他の Windows ツールを使用して、レジストリを直接編集するのではなく、タスクを実行します。 レジストリを編集する必要がある場合は、細心の注意が必要です。
>

診断エントリのログ記録レベルを変更するには

1. [ **Start**  >  **実行**の開始] をクリックし > **regedit** > [ **OK**] をクリックします。
2. ログインを設定するエントリに移動します。
   * 例: HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics
3. エントリをダブルクリックし、[ **Base**] で [ **Decimal**] をクリックします。
4. [**値**] に**0** ~ **5**の整数を入力し、[ **OK]** をクリックします。
