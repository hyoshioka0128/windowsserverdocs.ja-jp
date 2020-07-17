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
ms.technology: identity-adds
ms.openlocfilehash: b9e1cf812234bc3b0bd81db7045ed83208f3a0ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824365"
---
# <a name="ad-ds-troubleshooting"></a>AD FS のトラブルシューティング

>適用対象: windows Server 2019、Windows Server 2016、Windows Server 2012 R2

ここでは、Active Directory レプリケーション中に発生する可能性のある問題を診断および修正するためのトラブルシューティングの推奨事項と手順について説明します。 ディレクトリサービスのイベントログエントリに応答する方法と、Repadmin.exe や Dcdiag.exe などのツールで報告される可能性があるメッセージの解釈方法に焦点を当てています。

Repadmin.exe および Dcdiag.exe は、Windows Server 2012 R2 以降のバージョンを実行しているすべてのドメインコントローラーで使用できます。 これらのツールを使用して問題のトラブルシューティングを行う方法の詳細については、次の記事を参照してください。

- [トラブルシューティングのためにコンピューターを構成する Active Directory](../manage/troubleshoot/Configuring-a-Computer-for-Troubleshooting.md)
- [Active Directory レプリケーションの問題のトラブルシューティングに関するページ](../manage/troubleshoot/Troubleshooting-Active-Directory-Replication-Problems.md)

もう1つの便利なテクノロジは、Windows イベントトレーシング (ETW) です。 ETW を使用して、ドメインコントローラー間の LDAP 通信のトラブルシューティングを行うことができます。 詳細については、「 [ETW を使用した LDAP 接続のトラブルシューティング](../manage/troubleshoot/troubleshoot-ldap-using-etw.md)」を参照してください。

また、Windows 10 を実行しているメンバーサーバーにリモートサーバー管理ツール (RSAT) をインストールすることもできます。 RSAT のインストール方法の詳細については、「[リモートサーバー管理ツール](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)」を参照してください。
