ファブリックのドメインの名前解決を構成する多くの方法はあります。 1 つの簡単な方法では、ファブリックの dns 条件付けフォワーダーのゾーンを設定します。 このゾーンを設定するには、fabric の DNS サーバーで管理者特権での Windows PowerShell コンソールで次のコマンドを実行します。 名前と、環境に応じて以下の Windows PowerShell 構文内のアドレスに置き換えてください。 HGS の追加ノードのマスター サーバーを追加します。

```
Add-DnsServerConditionalForwarderZone -Name 'bastion.local' -ReplicationScope "Forest" -MasterServers <IP addresses of HGS server>
```

<!-- Appears in guarded-fabric-configuring-fabric-dns-ad.md and guarded-fabric-configuring-fabric-dns.md and set-up-hgs-for-always-encrypted-in-sql-server.md
-->    