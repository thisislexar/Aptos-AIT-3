<h1 align="center">Aptos AIT-3 için Fullnode Kurulumu
  
# Öncelikle şunu belirteyim, fullnode kurmak zorunlu değil. Optional olarak belirtilmiş, fakat yine de rehber hazırladım. Ayrıca hem Fullnode hem de validator kuracaksanız, farklı serverlarda kurmanız önerilmiş. Öyle yapın. Sorularınız için: [LossNode Chat](https://t.me/LossNode)

  
 # Detaylar: [Aptos Fullnode](https://aptos.dev/nodes/full-node/fullnode-for-devnet)
  ![image](https://user-images.githubusercontent.com/101462877/185744298-9d88ce04-406d-47ee-8478-0bf32b00bf55.png)
  
 # Fullnode için sistem gereksinimleri bu şekilde belirtilmiş.
  ![image](https://user-images.githubusercontent.com/101462877/185744951-9889f322-b9fa-4f3f-b439-27a10a071002.png)


 # Başlayalım. İlk olarak sunucumuzu güncelliyoruz.
  
  ```
  sudo apt update && sudo apt upgrade -y
  ```
# Docker yüklüyoruz.
  
  ```
sudo apt-get install ca-certificates curl gnupg lsb-release -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
  ```
  
  
# Docker compose yüklüyoruz.
  
  ```
apt install jq
docker_compose_version=$(wget -qO- https://api.github.com/repos/docker/compose/releases/latest | jq -r ".tag_name")
sudo wget -O /usr/bin/docker-compose "https://github.com/docker/compose/releases/download/${docker_compose_version}/docker-compose-`uname -s`-`uname -m`"
sudo chmod +x /usr/bin/docker-compose
  ```
  
  
# Fullnode'u yüklemek için yeni bir klasör oluşturuyoruz ve klasörün içine giriyoruz.
  ```
  mkdir ~/aptos-fullnode && cd ~/aptos-fullnode
  ```
  
# Aptos fullnode'unu yüklüyoruz.
  ```
wget -qO docker-compose.yaml https://raw.githubusercontent.com/aptos-labs/aptos-core/main/docker/compose/aptos-node/docker-compose-fullnode.yaml
wget -qO fullnode.yaml https://raw.githubusercontent.com/aptos-labs/aptos-core/main/docker/compose/aptos-node/fullnode.yaml
  ```
  
# Burayı dikkatli yapalım, `fullnode.yaml` dosyasının içine girip birkaç bir şey değiştireceğiz.
```
nano /root/aptos-fullnode/fullnode.yaml
```
![image](https://user-images.githubusercontent.com/101462877/185746263-f8bcac74-0650-40a0-ab0d-4ac024dafd26.png)
  
 Dosyanın içi böyle görünecektir, görselde anlatıldığı gibi ilgili kısmı kendi sunucu IP adresimiz ile değiştiriyoruz.
  
  Ardından dosyayı kapatmak için sırasıyla:
  
  - Ctrl + X
  - Y
  - Enter tuşlarına basıyoruz.

  
  Ardından `genesis` ve `waypoint.txt` dosyalarını indirelim.
  
  ```
curl -O https://devnet.aptoslabs.com/genesis.blob
curl -O https://devnet.aptoslabs.com/waypoint.txt
```

Bu kısımda WinSCP ile Validator node'umuza bağlanıp gerekli bağlantıları yapmamız gerekiyor. Bunun için ilk önce [Validator Node Kurulumu](https://github.com/thisislexar/Aptos-AIT-3/blob/main/validator.md)'na gidip Validator node'unuzu kurun. Ardından aşağıdaki işlemlerle devam edin.
