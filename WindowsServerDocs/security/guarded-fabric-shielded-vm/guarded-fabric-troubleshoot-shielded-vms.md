---
title: シールドされた Vm のトラブルシューティング
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 10/3/2018
ms.openlocfilehash: 6bcc32aae736a927576de28a15ca532279d4753b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944012"
---
# <a name="troubleshoot-shielded-vms"></a>シールドされた Vm のトラブルシューティング

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

Windows Server バージョン1803以降では、完全にシールドされた Vm に対して、仮想マシン接続 (VMConnect) の拡張セッションモードと PS Direct が再度有効になります。 仮想化管理者は vm にアクセスするために VM ゲストの資格情報を必要としますが、これにより、ネットワーク構成が切断されたときに、ホスト側がシールドされた VM のトラブルシューティングを簡単に行うことができます。

シールドされた Vm に対して VMConnect と PS Direct を有効にするには、Windows Server バージョン1803以降を実行している Hyper-v ホストに移動するだけです。 これらの機能を許可する仮想デバイスは、自動的に再び有効になります。 シールドされた VM が、以前のバージョンの Windows Server を実行しているホストに移動した場合、VMConnect と PS Direct は再び無効になります。

ホストに VM へのアクセス権があり、元の動作に戻す必要がある場合、セキュリティを重視するお客様には、ゲスト OS で次の機能を無効にする必要があります。

- VM で PowerShell ダイレクトサービスを無効にします。

  ```powershell
  Stop-Service vmicvmsession
  Set-Service vmicvmsession -StartupType Disabled
  ```

- VMConnect 拡張セッションモードは、ゲスト OS が Windows Server 2019 または Windows 10 バージョン1809以降である場合にのみ無効にすることができます。 VMConnect 拡張セッションコンソール接続を無効にするには、VM に次のレジストリキーを追加します。

  ```
  reg add "HKLM\Software\Microsoft\Virtual Machine\Guest" /v DisableEnhancedSessionConsoleConnection /t REG_DWORD /d 1
  ```
