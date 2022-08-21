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

  
Bu kısımda WinSCP ile Validator node'umuza bağlanıp gerekli bağlantıları yapmamız gerekiyor. Bunun için ilk önce [Validator Node Kurulumu](https://github.com/thisislexar/Aptos-AIT-3/blob/main/validator.md)'na gidip Validator node'unuzu kurun. Ardından aşağıdaki işlemlerle devam edin.

  # WinSCP (mac kullanıyorsanız Cyberduck)'yi açalım. Eğer WinSCP bilgisayarınızda yüklü değilse [buradan](https://winscp.net/eng/index.php) indirebilirsiniz. WinSCP ile Validator node'umuza bağlanalım.
  ![image](https://user-images.githubusercontent.com/101462877/185781466-fb1e7de3-8caa-4d93-9719-7f505ebe2fa7.png)
  
Aşağıdaki görselde gördüğüz gibi `keys`, `genesis.blob` ve `waypoint.txt` dosyalarını bilgisayarımıza kopyalayalım, bunları Fullnode'umuza aktaracağız. 
  
  ![image](https://user-images.githubusercontent.com/101462877/185781618-a49de870-4cb7-45db-8b4d-ef30a43cbc9c.png)
  
  WinSCP ile bu sefer Fullnode'umuza bağlanalım, kopyaladığımız dosyaları Fullnode içerisindeki `aptos-fullnode` dosyasının içine aktaralım.
  ![image](https://user-images.githubusercontent.com/101462877/185781722-1f6d36d5-7a69-4ebe-b0a7-2a61ac474ea9.png)

  
 # Ardından terminalimize geri dönelim ve node'u başlatalım.
  ```
 docker run --pull=always --rm -p 8080:8080 -p 9101:9101 -p 6180:6180 -v $(pwd):/opt/aptos/etc -v $(pwd)/data:/opt/aptos/data --workdir /opt/aptos/etc --name=aptos-fullnode aptoslabs/validator:devnet aptos-node -f /opt/aptos/etc/public_full_node.yaml
```
  ![image](https://user-images.githubusercontent.com/101462877/185781830-96c04be5-0a2c-4412-800f-84ec0330022e.png)

  Bu kısım biraz uzun sürebilir, tamamlanmasını bekleyelim.
  
  # Şimdi tekrar Validator node'umuza terminalden bağlanalım ve Fullnode'umuzu Validator node'umuza bağlayalım.
```
aptos genesis set-validator-configuration \
    --local-repository-dir ~/$WORKSPACE \
    --username $NODENAME \
    --owner-public-identity-file ~/$WORKSPACE/keys/public-keys.yaml \
    --validator-host $PUBLIC_IP:6180 \
    --stake-amount 100000000000000 \
    --full-node-host <FULLNODE_SUNUCU_IP>:6182
```
- Bu kısımda `<FULLNODE_SUNUCU_IP>` kısmını FULLNODE SUNUCU IP'niz ile değiştirerek girin.
  
  ![image](https://user-images.githubusercontent.com/101462877/185782353-f2e49169-4215-43da-b522-870ee987291a.png)

  Görseldeki gibi `"Result": "Success"` çıktısını aldıysanız olmuştur.
  # Ardından Validator node'umuzu aşağıdaki komutla tekrar başlatalım.
  
```
cd ~/$WORKSPACE
docker-compose restart
```
  # Kurulum bu kadardı, aşağıya Fullnode için gerekli olabilecek bazı komutlar bırakıyorum.
  
  ## Fullnode'unuzu tekrar başlatmak için kod:
  ```
  docker restart aptos-fullnode-fullnode-1 
  ```
  
  ## Fullnode'unuzda logları kontrol etmek için kod:

```
docker logs -f aptos-fullnode-fullnode-1 --tail 50
```

# Senkronize durumunu kontrol etmek için kod:

```
curl 127.0.0.1:9101/metrics 2> /dev/null | grep aptos_state_sync_version | grep type
``` 
