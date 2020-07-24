---
title: ネゴシエーション、セッション設定、ツリー接続のエラー
description: ネゴシエート、セッションのセットアップ、およびツリー接続のエラーのトラブルシューティングを行う方法について説明します。
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 2bad602f934d844074ee96df06bf9234fdbf943f
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961164"
---
# <a name="negotiate-session-setup-and-tree-connect-failures"></a>ネゴシエーション、セッション設定、ツリー接続のエラー

この記事では、SMB ネゴシエート、セッションセットアップ、およびツリー接続要求中に発生したエラーのトラブルシューティング方法について説明します。

## <a name="negotiate-fails"></a>ネゴシエートに失敗

Smb サーバーは、smb クライアントから SMB ネゴシエート要求を受信します。 接続がタイムアウトし、60秒後にリセットされます。 約200マイクロ秒後に ACK メッセージが表示される場合があります。

この問題は、多くの場合、ウイルス対策プログラムによって発生します。

Windows Server 2008 R2 を使用している場合は、この問題の修正プログラムがあります。 SMB クライアントと SMB サーバーが最新の状態であることを確認します。

## <a name="session-setup-fails"></a>セッションの設定が失敗する

Smb サーバーは smb クライアントから SMB セッションセットアップ要求を受信し \_ ましたが、応答できませんでした。

サーバーの完全修飾ドメイン名 (FQDN) またはネットワーク基本入出力システム (NetBIOS) 名が、汎用名前付け規則 (UNC) パスに含まれる場合、Windows は認証に Kerberos を使用します。

ネゴシエート応答の後に、サーバーの Common Internet File System (CIFS) サービスプリンシパル名 (SPN) の Kerberos チケットを取得しようとします。 SMB クライアントがトークンを取得しているときに Kerberos エラーが発生していないことを確認するには、TCP ポート88の Kerberos トラフィックを確認します。

> [!NOTE]
> Kerberos 事前認証中に発生したエラーは問題ありません。 Kerberos 事前認証 (認証が機能しないインスタンス) の後に発生するエラーは、SMB の問題の原因となったエラーです。

さらに、次のチェックを行います。

- SMB セッションセットアップ要求のセキュリティ blob を調べ \_ て、正しい資格情報が送信されていることを確認してください。

- SMB サーバー名のセキュリティ強化を無効にしてください (**SmbServerNameHardeningLevel = 0**)。

- CNAME DNS レコードを介してアクセスされるときに、SMB サーバーに SPN があることを確認します。

- SMB 署名が機能していることを確認します。 (これは、以前のサードパーティ製デバイスでは特に重要です)。

## <a name="tree-connect-fails"></a>ツリーの接続に失敗する

ユーザーアカウントの資格情報に、共有フォルダーと NT ファイルシステム (NTFS) の両方のアクセス許可があることを確認します。

一般的なツリー接続エラーの原因については、「 [3.3.5.7 受信 SMB2 Tree \_ connect Request](/openspecs/windows_protocols/ms-smb2/652e0c14-5014-4470-999d-b174d7b2da87)」を参照してください。 2つの一般的なステータスコードの解決策を次に示します。

\[状態 \_ 無効 \_ ネットワーク \_ 名\]

サーバーに共有が存在し、SMB クライアント要求に正しく入力されていることを確認してください。

\[ステータス \_ へのアクセスが拒否され \_ ました\]

共有によって使用されているディスクとフォルダーが存在し、アクセス可能であることを確認します。

SMBv3 以降を使用している場合は、サーバーと共有に暗号化が必要かどうかを確認してください。ただし、クライアントでは暗号化がサポートされていません。 これを行うには、次の操作を実行します。

- 次のコマンドを実行して、サーバーを確認します。

  ```PowerShell
  Get-SmbServerConfiguration | select Encrypt*
  ```

  EncryptData と RejectUnencryptedAccess が true の場合、サーバーは暗号化を必要とします。

- 次のコマンドを実行して、共有を確認します。

  ```PowerShell
  Get-SmbShare | select name, EncryptData  
  ```

  共有で EncryptData が true であり、サーバーで RejectUnencryptedAccess が true である場合、共有には暗号化が必要です。

トラブルシューティングの際には、次のガイドラインに従ってください。

- Windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows では、クライアント側の暗号化 (SMBv3 以降) がサポートされています。

- Windows 7、windows Server 2008 R2 以前のバージョンの Windows では、クライアント側の暗号化はサポートされていません。

- Samba とサードパーティデバイスは、暗号化をサポートしていない可能性があります。 詳細については、製品ドキュメントを参照してください。

## <a name="references"></a>リファレンス

詳細については、次の記事を参照してください。

[3.3.5.4 SMB2 NEGOTIATE 要求を受信しています](/openspecs/windows_protocols/ms-smb2/b39f253e-4963-40df-8dff-2f9040ebbeb1)

[3.3.5.5 SMB2 SESSION セットアップ要求を受信しています \_](/openspecs/windows_protocols/ms-smb2/e545352b-9f2b-4c5e-9350-db46e4f6755e)

[3.3.5.7 SMB2 TREE \_ CONNECT 要求の受信](/openspecs/windows_protocols/ms-smb2/652e0c14-5014-4470-999d-b174d7b2da87)
