---
title: ネゴシエーションの検証中に TCP 接続が中止されました
description: Validate Negotiate 中に TCP 接続が中止されたときに、SMB の問題のトラブルシューティングを行う方法について説明します。
author: Deland-Han
manager: dcscontentpm
audience: ITPro
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 3455b4ac0a2706f80702378dda02c1877af219ca
ms.sourcegitcommit: 8cf04db0bc44fd98f4321dca334e38c6573fae6c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75654623"
---
# <a name="tcp-connection-is-aborted-during-validate-negotiate"></a>ネゴシエーションの検証中に TCP 接続が中止されました

SMB の問題のネットワークトレースで、Negotiate の検証プロセス中に TCP リセットが中止されたことがわかります。 この記事では、状況をトラブルシューティングする方法について説明します。

## <a name="cause"></a>原因

この問題は、ネゴシエーションの検証に失敗した場合に発生する可能性があります。 これは通常、WAN アクセラレータによって元の SMB ネゴシエートパケットが変更されるために発生します。

Microsoft では、何らかの理由で Negotiate パケットの検証を変更することができなくなりました。 これは、この動作によって重大なセキュリティリスクが生じるためです。

Negotiate パケットの検証には、次の要件が適用されます。

- ネゴシエートの検証プロセスでは、FSCTL\_VALIDATE\_NEGOTIATE\_INFO コマンドを使用します。

- ネゴシエーションの検証応答には署名が必要です。 それ以外の場合、接続は中止されます。

- FSCTL\_VALIDATE\_NEGOTIATE\_情報メッセージをネゴシエートメッセージに比較して、何も変更されていないことを確認する必要があります。

## <a name="workaround"></a>回避策

ネゴシエートの検証プロセスを一時的に無効にすることができます。 これを行うには、次のレジストリサブキーを見つけます。

**HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\Parameters**

**Parameters**キーの下で、 **RequireSecureNegotiate**を**0**に設定します。

Windows PowerShell では、次のコマンドを実行してこの値を設定できます。

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecureNegotiate -Value 0 -Force
```

> [!NOTE]
> Windows 10、Windows Server 2016、またはそれ以降のバージョンの Windows では、ネゴシエートの検証プロセスを無効にすることはできません。

クライアントまたはサーバーが Negotiate Negotiate コマンドをサポートできない場合は、SMB 署名が必要になるように設定することで、この問題を回避できます。 SMB 署名は、Validate Negotiate よりも安全性が高いと見なされます。 ただし、署名が必要な場合は、パフォーマンスが低下する可能性もあります。

## <a name="reference"></a>辞書/リファレンス

詳しくは、次の記事をご覧ください。

[3.3.5.15.12 Negotiate 情報の検証要求の処理](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/0b7803eb-d561-48a4-8654-327803f59ec6)

[3.2.5.14.12 Negotiate 情報の検証応答の処理](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/6a5bc90d-3c08-4498-905b-e7dab30b2e0e)
