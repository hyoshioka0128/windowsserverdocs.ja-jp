---
title: DirectAccess の展開の前提条件
description: このトピックでは、Windows Server 2016 での DirectAccess 展開の前提条件について説明します。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57c7e039-42ef-4909-867a-b5f669c9e74e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 14da51a2617764f2ee11eedcbc7a4e10b3b0da15
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309314"
---
# <a name="prerequisites-for-deploying-directaccess"></a>DirectAccess の展開の前提条件

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次の表は、構成ウィザードを使用して DirectAccess を展開するために必要な前提条件を示しています。  
  
|||  
|-|-|  
|シナリオ|前提条件|  
|[はじめにウィザードを使用して単一の DirectAccess サーバーを展開する](../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|-すべてのプロファイルで Windows ファイアウォールを有効にする必要があります。<br /><br />-Windows 10&reg;を実行しているクライアントでのみサポートされています。 <br />              Windows&reg; 8、Windows&reg; 8.1 Enterprise。<br /><br />-公開キー基盤は必要ありません。<br /><br />-2 要素認証の展開ではサポートされていません。 認証にはドメインの資格情報が必要です。<br /><br />-現在のドメイン内のすべてのモバイルコンピューターに DirectAccess を自動的に展開します。<br /><br />-インターネットへのトラフィックは、DirectAccess を経由しません。 強制トンネルの構成はサポートされません。<br /><br />-DirectAccess サーバーは、ネットワークロケーションサーバーです。<br /><br />-ネットワークアクセス保護 (NAP) はサポートされていません。<br /><br />-DirectAccess 管理コンソールまたは Windows PowerShell コマンドレット以外の機能を使用してポリシーを変更することはできません。<br /><br />-マルチサイト構成の場合、または今後は、 [「詳細設定を使用した単一の DirectAccess サーバーの展開](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)」のガイダンスに従ってください。|  
|[詳細設定を使用して単一の DirectAccess サーバーを展開する](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)|-公開キー基盤を展開する必要があります。<br />    詳細については、「[テストラボガイドミニモジュール: Windows Server 2012 用の基本的な PKI](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)」を参照してください。<br /><br />-すべてのプロファイルで Windows ファイアウォールを有効にする必要があります。<br /><br />次のサーバーオペレーティングシステムでは、DirectAccess がサポートされています。<br /><br />-Windows Server 2016 のすべてのバージョンを DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。<br />-Windows Server 2012 R2 のすべてのバージョンを DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。<br />-Windows Server 2012 のすべてのバージョンを DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。<br />-Windows Server 2008 R2 のすべてのバージョンを DirectAccess クライアントまたは DirectAccess サーバーとして展開できます。<br /><br />次のクライアントオペレーティングシステムでは、DirectAccess がサポートされています。<br /><br />-Windows 10&reg; Enterprise<br />-Windows 10&reg; Enterprise 2015 Long Term Servicing Branch (LTSB)<br />-Windows&reg; 8 および 8.1 Enterprise<br />-Windows&reg; 7 Ultimate<br />-Windows&reg; 7 Enterprise<br /><br />-Force トンネルの構成は、KerbProxy 認証ではサポートされていません。<br /><br />-DirectAccess 管理コンソールまたは Windows PowerShell コマンドレット以外の機能を使用してポリシーを変更することはできません。<br /><br />-NAT64/DNS64 と IPHTTPS サーバーロールを別のサーバーに分離することはサポートされていません。|  
  


