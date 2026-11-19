# Raspberry Pi 5用 USB Wi-Fiドライバ別添パック

`TinyBox.tar.gz`に含まれていた以下のアーカイブを、内容を変更せず分離しています。

- rtl8852au.tar.gz
- rtl8812au.tar.gz
- rtw89.tar.gz
- rtl8852bu.tar.gz

本体は内蔵Wi-FiなどOSが認識する機器を使います。USB機器に追加ドライバが必要なときだけ利用します。元のラズパイ版の一律4種類ビルドから、選択式へ変更したものです。

```bash
tar -xzf TinyBox-RPi5-wifi-drivers.tar.gz
cd TinyBox-RPi5-wifi-drivers

# ハッシュ確認と一覧表示だけ。OS変更なし
python3 install-driver.py

# 例：必要なドライバだけをビルド・導入
sudo python3 install-driver.py --install rtl8852au
```

実行中カーネルと一致する`linux-headers-$(uname -r)`を使用します。最新番号の別カーネル用ヘッダーへ勝手に切り替えません。対応するヘッダーがaptにない場合は停止します。

既存モジュールの強制アンロードは行いません。必要なら導入後に再起動するか、明示的な`--load`で対象モジュールをロードします。

Ubuntu 24.04/26.04のARM64・Pi5以外では導入を停止しますが、OS判定に合格したことはドライバソースのカーネル互換性を保証しません。ソースを最新カーネルへ移植したものではありません。ビルド・AP/IBSS機能・通信は各実機で確認してください。

この補助処理は失敗時停止を行いますが、ドライバの旧版復元・自動ロールバック機能はありません。元ソースのLICENSE等は各アーカイブ内に保持しています。
