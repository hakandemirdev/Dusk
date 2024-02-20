# Dusk

<img src="https://github.com/hakandemirdev/Dusk/blob/d33e021854f35b38bb1b835c18f97e7973ce4eb6/dusk-network2.jpg" width="auto">

[Dusk Explorer](https://explorer.dusk.network)
[Discord](https://discord.com/invite/dusknetwork)
[Dusk Web Wallet](https://wallet.dusk.network/)

Öncelikle işletim sistemimizi güncelliyoruz.Ubuntu 22.04.3 LTS üzerine kurdum.
```
sudo apt-get update  && sudo apt-get upgrade
```
Port ayarlarımızı yapıyoruz.
```
sudo ufw enable
sudo ufw allow 22
sudo ufw allow 9000/udp
sudo ufw allow 8080/tcp
```
Rusk Yüklüyoruz
```
curl --proto '=https' --tlsv1.2 -sSfL https://github.com/dusk-network/itn-installer/releases/download/v0.1.0/itn-installer.sh | sudo sh
```
Aşağıdaki komutu girmeden önce bir cüzdan oluşturmamız gerekiyor. [Buradan](https://wallet.dusk.network/) bir cüzdan oluşturuyor ve mnemonic'lerimizi kaydediyoruz.
Aşağıdaki komutla cüzdanımızı içe aktarıyoruz. Bizden mnemonic'leri yazmamızı isteyecek. Küçük harflerle mnemonic kelimelerimiz yazıyoruz.
Daha sonra bizden cüzdanımız için şifre oluşturmamızı isteyecek, bir şifre oluşturuyor ve şifreyi tekrar giriyoruz.
```
rusk-wallet restore
```
İçe aktardığımız cüzdan için konsensus key oluşturuyoruz.Cüzdan şifremizi girdikten sonra şifreleme anahtarı için bir şifre daha belirleyip yazıyoruz.
```
rusk-wallet export -d /opt/dusk/conf -n consensus.keys
```
Ortam değişkenlerini ayarlıyoruz.
```
sh /opt/dusk/bin/setup_consensus_pwd.sh
```
Artık Rusk'ı başlatabiliriz.
```
service rusk start
```
Senkronize olup olmadığını kontrol etmek için aşağıdaki komutu kullanabiliriz. [Explorer](https://explorer.dusk.network)
```
grep "block accepted" /var/log/rusk.log
```
Dusk [Discord](https://discord.com/invite/dusknetwork) kanalına gidiyoruz ve "Dusk Testnet Faucet Bot" üzerine sağlık tıklayıp "Mesaj Gönder" butonuna basıyoruz.
!dusk yazdıktan sonra bot cüzdan adresimizi isteyecek, cüzdan adresimizi giriyoruz.
Cüzdanımıza test tokenları geldikten ve nodumuz senkronize olduktan sonra tokenlarımızı stake ediyoruz.
```
rusk-wallet stake --amt 1000 # Minimum 1000 olması gerekiyoruz, daha fazla token da stake edebiliriz.
```
Stake durumunu aşağıdaki komutla kontrol edebiliriz.
```
rusk-wallet stake-info
```
Nodumuzun blok oluşturup oluşturmadığını aşağıdaki komutla öğrenebiliriz.
```
grep "execute_state_transition" /var/log/rusk.log | tail -n 5
```
