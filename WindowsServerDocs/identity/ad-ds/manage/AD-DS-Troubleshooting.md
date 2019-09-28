---
ms.assetid: fd3bc84a-48eb-4f00-9dc2-846bf2c2668b
title: AD FS のトラブルシューティング
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 995ba44a64ae022b52213b9c912f94144d4c2543
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369328"
---
# <a name="ad-ds-troubleshooting"></a>AD FS のトラブルシューティング

>適用先:Windows Server 2016、Windows Server 2012 R2

ここでは、Active Directory レプリケーションで発生する可能性のある問題を診断および修正するためのトラブルシューティングの推奨事項と手順について説明します。

このコンテンツでは、主に、Repadmin.exe および Dcdiag.exe ツールによって報告される可能性がある、ディレクトリサービスのイベントログメッセージとツールベースのエラーメッセージへの応答に焦点を当てています。 これらのツールは、Windows Server 2016 または 2012 R2 を実行しているすべてのドメインコントローラーで使用できます。 また、Windows 10 を実行しているメンバーサーバーにリモートサーバー管理ツール (RSAT) をインストールすることもできます。

RSAT のインストールの詳細については、「[リモートサーバー管理ツール](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)」を参照してください。

[トラブルシューティングのためにコンピューターを構成する Active Directory](../manage/troubleshoot/Configuring-a-Computer-for-Troubleshooting.md)

[Active Directory レプリケーションの問題のトラブルシューティングに関するページ](../manage/troubleshoot/Troubleshooting-Active-Directory-Replication-Problems.md)
