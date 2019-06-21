---
title: DirectAccess の展開の前提条件
description: このトピックでは、Windows Server 2016 での DirectAccess の展開の前提条件を提供します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57c7e039-42ef-4909-867a-b5f669c9e74e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f77df438ba2b282101a031b4ff4d145286cf3e94
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283625"
---
# <a name="prerequisites-for-deploying-directaccess"></a>DirectAccess の展開の前提条件

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

次の表では、構成ウィザードを使用して DirectAccess を展開するために必要な前提条件を示します。  
  
|||  
|-|-|  
|シナリオ|前提条件|  
|[作業の開始ウィザードを使用して単一の DirectAccess サーバーの展開します。](../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|のすべてのプロファイルで Windows ファイアウォールを有効にする必要があります。<br /><br />で Windows 10 を実行しているクライアントのみサポートされている&reg;、 <br />              Windows&reg; 8、および Windows&reg; 8.1 Enterprise。<br /><br />-公開キー基盤は必要ありません。<br /><br />-2 要素認証を展開するためにサポートされていません。 認証にはドメインの資格情報が必要です。<br /><br />-自動的に現在のドメイン内のすべてのモバイル コンピューターに DirectAccess を展開します。<br /><br />のインターネットへトラフィックは、DirectAccess 経由は説明しません。 強制トンネルの構成はサポートされません。<br /><br />-DirectAccess サーバーは、ネットワーク ロケーション サーバーです。<br /><br />-ネットワーク アクセス保護 (NAP) がサポートされていません。<br /><br />-DirectAccess 管理コンソールまたは Windows PowerShell コマンドレット以外の機能を使用してポリシーを変更することはできません。<br /><br />マルチサイト構成では、現在または今後は、最初のガイダンスに従って[詳細設定を使用する単一の DirectAccess サーバーをデプロイ](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)します。|  
|[詳細設定を使用して単一の DirectAccess サーバーを展開する](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)|-公開キー基盤を展開する必要があります。<br />    詳細については、次を参照してください。[テスト ラボ ガイド ミニ モジュール。Windows Server 2012 の基本 PKI](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)します。<br /><br />-Windows ファイアウォールは、すべてのプロファイルで有効にする必要があります。<br /><br />次のサーバー オペレーティング システムでは、DirectAccess をサポートします。<br /><br />-DirectAccess クライアントまたは DirectAccess サーバーとして Windows Server 2016 のすべてのバージョンをデプロイできます。<br />-Windows Server 2012 R2 の DirectAccess クライアントと DirectAccess サーバーのすべてのバージョンをデプロイできます。<br />-Windows Server 2012 の DirectAccess クライアントと DirectAccess サーバーのすべてのバージョンをデプロイできます。<br />-Windows Server 2008 R2 の DirectAccess クライアントと DirectAccess サーバーのすべてのバージョンをデプロイできます。<br /><br />次のクライアント オペレーティング システムでは、DirectAccess をサポートします。<br /><br />Windows 10&reg; Enterprise<br />Windows 10&reg; Servicing Branch (LTSB) Enterprise 2015 の時間の長い用語<br />-Windows&reg; 8 および 8.1 Enterprise<br />-Windows&reg; 7 Ultimate<br />-   Windows&reg; 7 Enterprise<br /><br />-強制トンネルの構成は KerbProxy 認証でサポートされていません。<br /><br />-DirectAccess 管理コンソールまたは Windows PowerShell コマンドレット以外の機能を使用してポリシーを変更することはできません。<br /><br />-Nat64/dns64 と IPHTTPS 別のサーバー上のサーバーの役割を分離することはサポートされていません。|  
  


