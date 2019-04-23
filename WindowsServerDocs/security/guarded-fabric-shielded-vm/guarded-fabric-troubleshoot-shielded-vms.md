---
title: シールドされた Vm をトラブルシューティングします。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 10/3/2018
ms.openlocfilehash: 13ff0dad1519d394ce74a91efbfcc9e2f237e4a5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850033"
---
# <a name="troubleshoot-shielded-vms"></a>シールドされた Vm をトラブルシューティングします。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

Windows Server バージョン 1803 以降では、拡張セッション モードの仮想マシン接続 (VMConnect) と PS ダイレクトは、完全にシールドされた Vm を再び有効にします。 VM ゲストの資格情報、VM へのアクセスを取得する必要があります、仮想化管理者が、ホストは、そのネットワークの構成が壊れている場合、シールドされた VM のトラブルシューティングが簡単になります。 します。

シールドされた Vm の VMConnect と PS ダイレクトを有効にする、単に移動 1803 以降のバージョンの Windows Server を実行する HYPER-V ホストにします。 これらの機能のための仮想デバイスは再自動的に有効にします。 シールドされた VM を移動する場合、実行するホストと Windows Server の以前のバージョン、VMConnect と PS の直接が再び無効にします。

セキュリティに影響するホスティング企業が、VM にアクセスすること、および動作を元に返される場合の心配をお客様には、ゲスト OS で、次の機能を無効にする必要があります。

- VM で PowerShell ダイレクト サービスを無効にします。

  ```powershell
  Stop-Service vmicvmsession
  Set-Service vmicvmsession -StartupType Disabled
  ```

- 場合、ゲスト OS は、少なくとも、VMConnect 拡張セッション モードを無効にできますのみ Windows Server 2019 または Windows 10、バージョンは 1809 します。 VMConnect の拡張セッションのコンソール接続を無効にする VM では、次のレジストリ キーを追加します。

  ```
  reg add "HKLM\Software\Microsoft\Virtual Machine\Guest" /v DisableEnhancedSessionConsoleConnection /t REG_DWORD /d 1
  ```
