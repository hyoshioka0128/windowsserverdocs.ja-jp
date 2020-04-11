---
title: 管理者のための Windows デスクトップ クライアント
description: Windows デスクトップ クライアントの情報は、主に管理者に役立ちます。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 09/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 202b39c33896f6b5e570c8abcf630dad436466c3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861425"
---
# <a name="windows-desktop-client-for-admins"></a>管理者のための Windows デスクトップ クライアント

>適用先:Windows 10 および Windows 7

このトピックでは、管理者にとって役に立つ Windows デスクトップ クライアントに関する追加情報を示します。 基本的な使用方法については、「[Windows デスクトップ クライアントの概要](windowsdesktop.md)」を参照してください。

## <a name="installation-options"></a>インストール オプション

ユーザーはダウンロード後にクライアントを直接インストールできますが、管理者が複数のデバイスに展開する場合は、他の方法でデバイスにクライアントを展開することもできます。 グループ ポリシーまたは Microsoft Endpoint Configuration Manager を使用して展開すると、コマンド ラインを使用してインストーラーをサイレント モードで実行できます。 デバイスごとまたはユーザーごとにクライアントを展開するには、次のコマンドを実行します。

### <a name="per-device-installation"></a>デバイスごとのインストール

```
msiexec.exe /I <path to the MSI> /qn ALLUSERS=1
```

### <a name="per-user-installation"></a>ユーザーごとのインストール

```
msiexec.exe /i `<path to the MSI>` /qn ALLUSERS=2 MSIINSTALLPERUSER=1
```

## <a name="configuration-options"></a>構成オプション

このセクションでは、このクライアントの新しい構成オプションについて説明します。

### <a name="configure-update-notifications"></a>更新プログラム通知を構成する

既定では、更新プログラムがあるたびにクライアントから通知されます。 通知をオフにするには、次のレジストリ情報を設定します。

- **キー:** HKLM\Software\Microsoft\MSRDC\Policies
- **型:** REG_DWORD
- **名前:** AutomaticUpdates
- **データ:** 0 = 通知を無効にする。 1 = 通知を表示する。

### <a name="configure-user-groups"></a>ユーザー グループを構成する

次のいずれかの種類のユーザー グループ用にクライアントを構成できます。これにより、クライアントがいつ更新プログラムを受け取るかが決まります。

#### <a name="insider-group"></a>Insider グループ

Insider グループは早期検証用であり、管理者と管理者によって選択されたユーザーで構成されます。 Insider グループは、テスト実行を行って、Public グループにリリースされる前に、パフォーマンスに影響する可能性がある更新プログラムの問題を検出します。

> [!NOTE]
> 更新プログラムをテストして問題を早期に発見するには、各組織のユーザーを Insider グループに含めることをお勧めします。

Insider グループでは、早期検証のために、毎月第 2 火曜日に新しいバージョンのクライアントがユーザーにリリースされます。 更新プログラムに問題がない場合は、2 週間後に Public グループにリリースされます。 Insider グループのユーザーは、更新プログラムの準備が整うたびに、更新プログラム通知を自動的に受け取ります。 クライアントに対する変更の詳細は、「[Windows デスクトップ クライアントの新機能](windowsdesktop-whatsnew.md)」で確認できます。

Insider グループのクライアントを構成するには、次のレジストリ情報を設定します。

- **キー:** HKLM\Software\Microsoft\MSRDC\Policies
- **型:** REG_SZ
- **名前:** ReleaseRing
- **データ:** insider

#### <a name="public-group"></a>Public グループ

このグループはすべてのユーザーが対象であり、最も安定したバージョンです。 このグループを構成するために何もする必要はありません。

Public グループは、毎月第 4 火曜日に、Insider グループによってテストされたバージョンのクライアントを受け取ります。 設定が有効になっている場合、Public グループのすべてのユーザーが更新プログラム通知を受け取ります。
