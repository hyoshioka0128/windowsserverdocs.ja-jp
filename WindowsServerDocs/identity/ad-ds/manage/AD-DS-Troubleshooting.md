---
ms.assetid: fd3bc84a-48eb-4f00-9dc2-846bf2c2668b
title: AD FS のトラブルシューティング
description: AD DS のトラブルシューティングセクションの概要
ms.author: joflore
author: MicrosoftGuyJFlo
manager: dcscontentpm
ms.date: 11/22/2019
ms.topic: article
ms.prod: windows-server
audience: Admin
ms.custom:
- CSSTroubleshoot
ms.technology: identity-adds
ms.openlocfilehash: 500ffe05fe75db99f98fda09b5f86b8547ea7e32
ms.sourcegitcommit: 30de12eebeb0fc79567d6bb6ab513692ea2415d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74853587"
---
# <a name="ad-ds-troubleshooting"></a>AD FS のトラブルシューティング

>適用対象: windows Server 2019、Windows Server 2016、Windows Server 2012 R2

ここでは、Active Directory レプリケーション中に発生する可能性のある問題を診断および修正するためのトラブルシューティングの推奨事項と手順について説明します。 ディレクトリサービスのイベントログエントリに応答する方法と、Repadmin.exe や Dcdiag.exe などのツールで報告される可能性があるメッセージの解釈方法に焦点を当てています。

Repadmin.exe および Dcdiag.exe は、Windows Server 2012 R2 以降のバージョンを実行しているすべてのドメインコントローラーで使用できます。 これらのツールを使用して問題のトラブルシューティングを行う方法の詳細については、次の記事を参照してください。

- [トラブルシューティングのためにコンピューターを構成する Active Directory](../manage/troubleshoot/Configuring-a-Computer-for-Troubleshooting.md)
- [Active Directory レプリケーションの問題のトラブルシューティングに関するページ](../manage/troubleshoot/Troubleshooting-Active-Directory-Replication-Problems.md)

もう1つの便利なテクノロジは、Windows イベントトレーシング (ETW) です。 ETW を使用して、ドメインコントローラー間の LDAP 通信のトラブルシューティングを行うことができます。 詳細については、「 [ETW を使用した LDAP 接続のトラブルシューティング](../manage/troubleshoot/troubleshoot-ldap-using-etw.md)」を参照してください。

また、Windows 10 を実行しているメンバーサーバーにリモートサーバー管理ツール (RSAT) をインストールすることもできます。 RSAT のインストール方法の詳細については、「[リモートサーバー管理ツール](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)」を参照してください。
