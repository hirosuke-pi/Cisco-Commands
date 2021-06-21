# Ciscoルーターコマンド早見表

- おすすめサイト

> https://beginners-network.com/

## モードを変更

### 特権モード
 
1. Router> `enable`

> Router> が Router# になる

### グローバルコンフィグレーションモード

1. Router# `configure terminal`

> Router# が Router(config)# になる

### ひとつ前のモードに戻る

1. Router(config)# `exit`

> Router(config)# が、 Router# になる


## ルーターの設定一覧を表示する

### 設定された項目を表示

- 参考サイト: https://beginners-network.com/cisco-catalyst-command/show-running-config.html

1. Router# `show running-config`

> 設定された項目一覧が表示される。[Space]キーで次のページが見られる

### RIPテーブルを表示

- 参考サイト: https://beginners-network.com/cisco-catalyst-command/show-ip-route.html

1. Router# `show ip route`

> ルーターに設定されたRIPテーブル一覧が表示される

### VLANの設定を表示

- 参考サイト: https://www.allied-telesis.co.jp/support/list/router/arx640s/comref_/docs/show_vlan-switch@010USEREXEC.html

1. Router# `show vlan-switch`

> ルーターのスイッチポートに設定されたVLANが表示される


## ポートにIPアドレスを設定
- 参考サイト: https://beginners-network.com/cisco-catalyst-command/ip-address.html

- ポートが"fastEthernet 0"で、"192.168.1.1"を設定する場合

1. Router(config)# `interface fastEthernet 0`
2. Router(config-if)# `ip address 192.168.1.1 255.255.255.0`
3. Router(config-if)# `no shutdown`
4. Router(config-if)# `exit`

> 削除する場合は、`no ip address 192.168.1.1 255.255.255.0` と入力する

- "192.168.1.4"の、ループバックアドレスを設定する

1. Router(config)# `interface loopback 0`
2. Router(config-if)# `ip address 192.168.1.4 255.255.255.0`
3. Router(config-if)# `exit`

> 削除する場合は、`no ip address 192.168.1.4 255.255.255.0` と入力する

## ルーティング設定

### 静的ルーティングの設定
- 参考サイト: https://beginners-network.com/cisco-catalyst-command/ip-route.html

- ネクストホップアドレス"192.168.1.2"から、"192.168.2.0"ネットワークに送信する

1. Router(config)# `ip route 192.168.2.0 255.255.255.0 192.168.1.2`

> 削除する場合は、`no ip route 192.168.2.0 255.255.255.0 192.168.1.2` と入力する


### 動的ルーティングの設定
- 参考サイト: https://beginners-network.com/cisco-catalyst-command/network-rip.html

- RIPを使って、"192.168.2.0"ネットワークと、"192.168.3.0"ネットワークをつなげる

1. Router(config)# `router rip`
2. Router(config-router)# `network 192.168.2.0`
3. Router(config-router)# `network 192.168.3.0`
4. Router(config-router)# `exit`

> 削除する場合は、`no network 192.168.2.0` と入力する

## VLAN設定

### VLANの作成
- 参考サイト: https://beginners-network.com/cisco-catalyst-command/vlan.html

- vlan10を作る

1. Router# `vlan database`
2. Router(vlan)# `vlan 10`

> VLAN設定を削除する場合は、 `delete vlan.dat` と入力する(再起動が必要)

### VLANの適応
- 参考サイト: https://beginners-network.com/catalyst_config_vlan.html

- ポートが"fastEthernet 3"で、"VLAN10"を設定する場合

1. Router(config)# `interface fastethernet 3`
2. Router(config-if)# `switchport access vlan 10`

> ちゃんと適応されているか `show vlan-switch` で確認しよう

### トランクリンクの設定

- ポート"fastEthernet 0"に設定する場合

1. Router(config)# `interface fastEthernet 0`
2. Router(config-if)# `swichport mode trunk`

> かんたんですね！