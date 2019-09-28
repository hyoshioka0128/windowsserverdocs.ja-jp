---
title: bootcfg
description: '**Bootcfg**の Windows コマンドのトピック-boot.ini ファイルの設定の構成、クエリ、または変更を行います。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3deb354c-5717-4066-bc79-b9323d559e44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d66296327a2221093e5434f69e15e7c55df1f6b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379846"
---
# <a name="bootcfg"></a>bootcfg

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Boot.ini ファイルの設定の構成、クエリ、または変更を行います。  
## <a name="syntax"></a>構文  
```  
bootcfg <parameter> [arguments...]  
```  
## <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|[bootcfg addsw](bootcfg-addsw.md)|指定したオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを追加します。|  
|[bootcfg copy](bootcfg-copy.md)|既存のブートエントリのコピーを作成します。これには、コマンドラインオプションを追加できます。|  
|[bootcfg dbg1394](bootcfg-dbg1394.md)|指定されたオペレーティングシステムエントリに対して1394ポートデバッグを構成します。|  
|[bootcfg debug](bootcfg-debug.md)|指定したオペレーティングシステムエントリのデバッグ設定を追加または変更します。|  
|[bootcfg default](bootcfg-default.md)|既定値として指定するオペレーティングシステムエントリを指定します。|  
|[bootcfg delete](bootcfg-delete.md)|boot.ini ファイルの **[オペレーティングシステム]** セクションにあるオペレーティングシステムのエントリを削除します。|  
|[bootcfg ems](bootcfg-ems.md)|ユーザーが、緊急管理サービスコンソールをリモートコンピューターにリダイレクトするための設定を追加または変更できるようにします。|  
|[bootcfg query](bootcfg-query.md)|Boot.ini の [ブートローダー] セクションと **[オペレーティングシステム]** セクションのエントリを照会して表示します。|  
|[bootcfg raw](bootcfg-raw.md)|boot.ini ファイルの **[オペレーティングシステム]** セクションのオペレーティングシステムエントリに、文字列として指定されたオペレーティングシステムの読み込みオプションを追加します。|  
|[bootcfg rmsw](bootcfg-rmsw.md)|指定したオペレーティングシステムエントリのオペレーティングシステムの読み込みオプションを削除します。|  
|[bootcfg timeout](bootcfg-timeout.md)|オペレーティングシステムのタイムアウト値を変更します。|  
