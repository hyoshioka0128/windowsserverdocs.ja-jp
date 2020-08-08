---
title: DirectAccess の展開の前提条件
description: このトピックでは、Windows Server 2016 での DirectAccess 展開の前提条件について説明します。
manager: brianlic
ms.topic: article
ms.assetid: 57c7e039-42ef-4909-867a-b5f669c9e74e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2025c2d90d9eef679bf8f51c18c9e1ba32123441
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87994954"
---
# <a name="prerequisites-for-deploying-directaccess"></a>DirectAccess の展開の前提条件

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次の表は、構成ウィザードを使用して DirectAccess を展開するために必要な前提条件を示しています。

|シナリオ|前提条件|
|-|-|
|[はじめにウィザードを使用して単一の DirectAccess サーバーを展開する](../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|-すべてのプロファイルで Windows ファイアウォールを有効にする必要があります。<p>-Windows 10 を実行しているクライアントでのみサポートされてい &reg; ます。 <br />              Windows &reg; 8 および windows &reg; 8.1 Enterprise。<p>-公開キー基盤は必要ありません。<p>-2 要素認証の展開ではサポートされていません。 認証にはドメインの資格情報が必要です。<p>-現在のドメイン内のすべてのモバイルコンピューターに DirectAccess を自動的に展開します。<p>-インターネットへのトラフィックは、DirectAccess を経由しません。 強制トンネルの構成はサポートされません。<p>-DirectAccess サーバーは、ネットワークロケーションサーバーです。<p>-ネットワークアクセス保護 (NAP) はサポートされていません。<p>-DirectAccess 管理コンソールまたは Windows PowerShell コマンドレット以外の機能を使用してポリシーを変更することはできません。<p>-マルチサイト構成の場合、または今後は、 [「詳細設定を使用した単一の DirectAccess サーバーの展開](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)」のガイダンスに従ってください。|
|[詳細設定を使用して単一の DirectAccess サーバーを展開する](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)|-公開キー基盤を展開する必要があります。<br /> 詳細については、「[テストラボガイドミニモジュール: Windows Server 2012 用の基本的な PKI](/answers/topics/windows-server-2012.html)」を参照してください。<p>-すべてのプロファイルで Windows ファイアウォールを有効にする必要があります。<p>次のサーバーオペレーティングシステムでは、DirectAccess がサポートされています。<p>-Windows Server 2016 のすべてのバージョンを DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。<br />-Windows Server 2012 R2 のすべてのバージョンを DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。<br />-Windows Server 2012 のすべてのバージョンを DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。<br />-Windows Server 2008 R2 のすべてのバージョンを DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。<p>次のクライアントオペレーティングシステムでは、DirectAccess がサポートされています。<p>-Windows 10 &reg; Enterprise<br />-Windows 10 &reg; Enterprise 2015 Long Term Servicing Branch (LTSB)<br />-Windows &reg; 8 および 8.1 Enterprise<br />-Windows &reg; 7 Ultimate<br />-Windows &reg; 7 Enterprise<p>-Force トンネルの構成は、KerbProxy 認証ではサポートされていません。<p>-DirectAccess 管理コンソールまたは Windows PowerShell コマンドレット以外の機能を使用してポリシーを変更することはできません。<p>-NAT64/DNS64 と IPHTTPS サーバーロールを別のサーバーに分離することはサポートされていません。|