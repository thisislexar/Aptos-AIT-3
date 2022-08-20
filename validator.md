<h1 align="center">Aptos AIT-3 için Validator Node Kurulumu

  ## Bu rehberde önemli Aptos testneti için validator kuruyor olacağız. Sorularınız için: [LossNode Chat](https://t.me/LossNode)
  
 ![image](https://user-images.githubusercontent.com/101462877/185746612-e3b69ea4-30bf-4326-b8c4-d78ce2b01970.png)

# Aptos için minimum sistem gereksinimleri aşağıdaki gibi belirtilmiş.

- CPU: 8 çekirdek
- RAM: 32GB RAM
- SSD: 300GB
  
  
  # Node kurmadan önce yapılması gereken adımlar var, bunları görsellerle anlatıyor olacağım. İlk 3 adım, aşağıdaki görselde belirtilmiş.
  ![image](https://user-images.githubusercontent.com/101462877/185747032-eb7aefa3-6c89-4a7a-9a99-dec759d05e78.png)

  
  # 1. adım ile başlıyoruz. [Aptos Community Sayfası](https://aptoslabs.com/community)'na gidelim. Sağ üstten `Sign In` diyelim ve Discord ile bağlanalım. [Discord](https://discord.gg/AaZk5MBQa3)'a daha önce katılmadıysanız mutlaka katılın.
  ![image](https://user-images.githubusercontent.com/101462877/185747061-ed942473-4c4d-4210-9e4b-92df648ff568.png)
![image](https://user-images.githubusercontent.com/101462877/185747081-58d23401-cec2-4a1b-b187-017829939e1e.png)

  
  # 2.adıma geçmeden önce Aptos için wallet kurmamız gerekiyor. Bu wallet şuan için Chrome Web Mağaza gibi platformlarda yok. Kendimiz indirip kuracağız. Görsellerle anlatıyorum.
  ## [Petra Wallet GitHub](https://github.com/aptos-labs/aptos-core/releases?q=wallet&expanded=true) sayfasına gidiyoruz. Ok ile gösterdiğim yere tıklayarak indiriyoruz.
  ![image](https://user-images.githubusercontent.com/101462877/185747191-ccadc26f-ef19-4e11-ba92-f01147696386.png)
## Ardından zip dosyasını indirdiğimiz klasöre gidiyoruz. Sağ tıklayıp burada ayıkla diyoruz. Ayıkladıktan sonra karşımıza `build` adında bir klasör çıkıyor.![image](https://user-images.githubusercontent.com/101462877/185747242-61718715-2b68-4c44-a2c9-d76d0b805f17.png)
## Şimdi hangi tarayıcıyı kullanıyorsak o tarayıcıyı açıyoruz, ben Brave üzerinden anlatacağım. Sırasıyla görseldeki butonlara tıklayalım.
  ![image](https://user-images.githubusercontent.com/101462877/185747391-d65dec8d-a11a-44e4-ba7e-98da296c35b2.png)
## Ardından sağ üstten geliştirici modunu açalım, ve az önce ayıkladığımız build klasörünü olduğu gibi tarayıcıya sürükleyelim. Kendisi uzantıyı ekleyecektir.
 ## Eklediğimiz wallet'ı açalım ve wallet kuralım. Bize verdiği kurtarma kelimelerini doğru bir şekilde not ettiğimizden emin olalım. Wallet bizim için önemli olacak.
  ![image](https://user-images.githubusercontent.com/101462877/185747445-29167329-ce50-4c05-807a-9fef0b10f7e4.png)

  ## Cüzdanı kurduktan sonra [AIT-3 için Kayıt Sayfası](https://aptoslabs.com/it3)'na gidelim ve cüzdanımızı bağlayalım.
  ![image](https://user-images.githubusercontent.com/101462877/185747537-b13126c8-94af-4a5c-9de4-01ef62bcd5dc.png)

  # 3. adım olarak yine [AIT-3 için Kayıt Sayfası](https://aptoslabs.com/it3)'na gidelim ve anketi dolduralım. Anketi özenli bir şekilde doldurduğunuza emin olun.
  
  ![image](https://user-images.githubusercontent.com/101462877/185748018-f8dfe635-9a1b-48d5-89d8-b32bb5dcff05.png)
  
  ## Anket ile birlikte ilk 3 adımı tamamlamış olduk. Şimdi diğer adımlara geçelim.
  
  ![image](https://user-images.githubusercontent.com/101462877/185748118-37ec5fa5-a339-4355-83b7-0b3f3f5e9aec.png)

  
  # 4. adımda node kurulumumuzu gerçekleştiriyoruz ve node'umuzu kayıt ediyoruz. Script ile kuracağız çünkü manuel işlemler biraz karmaşık. Hata almadan kurulum yapmak amacıyla script kullanacağız.
  
  
 ## Script kod ile direkt node'umuzu kuruyoruz.
  
  ```
  wget -qO aptos_validator.sh https://raw.githubusercontent.com/kj89/testnet_manuals/main/aptos/testnet/aptos_validator.sh && chmod +x aptos_validator.sh && ./aptos_validator.sh
  ```
  
 ## Ardından değişkenleri sisteme kaydetmek için bu kod ile devam ediyoruz.
  
 ```
source $HOME/.bash_profile
 ```
 
  ## Ayrıca bazı portları açmamız gerekiyor. Bunları açalım.
   ```
sudo ufw enable
 ```
   ```
ufw allow 80
 ```
  

  
  
  
 ## Node'u kontrol etmek için [bu siteye](https://node.aptos.zvalid.com/) gidelim.
  
  
  ![image](https://user-images.githubusercontent.com/101462877/185746854-15603254-b790-4e5d-80ef-d99228f6ff40.png)

  Bu kısıma Validator Node'umuzun sunucu IP'sini yazalım ve kontrol edelim.
  
  ![image](https://user-images.githubusercontent.com/101462877/185746873-b28e0be3-61a5-439c-ac91-49c651e7b27b.png)
  
Bu şekilde bir görüntü varsa başarılı bir şekilde kurmuşuz demektir.
  
 ## Node'umuzu başarıyla kurduk, şimdi Node'umuzu sisteme kayıt edeceğiz. Bunun için tekrar [AIT-3 için Kayıt Sayfası](https://aptoslabs.com/it3)'na gidiyoruz.
  
  ![image](https://user-images.githubusercontent.com/101462877/185748205-5209eadb-1c50-44de-889f-558406bf13e4.png)

  Şuan için henüz anketi doldurmadığım için bu kısımda buton bulunmuyor, fakat siz anketi doldurduktan sonra buradaki buton aktif olacaktır.
  
  ## Bu kısımda doldurmanız gereken yerler için verileri nereden alacağınızı anlatacağım. Boşlukları tek tek emin olarak doldurun, hatalı kayıt yapmak istemezsiniz.
  
  Kurduğumuz validator node'unda aşağıdaki komutu girelim:
  ```
cat ~/$WORKSPACE/keys/public-keys.yaml
  ```
  Ardından karşımıza çıkan dosyadaki veriler ile kayıt formunu dolduralım. Hangi boşluk için hangi veriyi girmeniz gerektiğini aşağıya bırakıyorum. Ayrıca, API PORT'u `8080` olarak geliyor, onu `80` olarak değiştirin.
  
  ![image](https://user-images.githubusercontent.com/101462877/185748364-40ef482b-a3e5-4825-a7c2-19b3fbe7478f.png)
  
  - `OWNER KEY`: Petra cüzdanınızın `Public Key`'i. Nasıl erişebileceğinizi aşağıdaki ss'lerde gösterdim.
  ![image](https://user-images.githubusercontent.com/101462877/185748436-3837fcba-b981-4f31-b0c5-18875d782163.png) ![image](https://user-images.githubusercontent.com/101462877/185748440-b9ac017c-ff45-4817-82d6-883a21b527b0.png)
- `CONSENSUS KEY`: Yukarıdaki komutla terminalde gördüğümüz consensus_public_key
- `CONSENSUS POP`: Yukarıdaki komutla terminalde gördüğümüz consensus_proof_of_possession 
- `ACCOUNT KEY`: Yukarıdaki komutla terminalde gördüğümüz account_public_key 
- `VALIDATOR NETWORK KEY`: Yukarıdaki komutla terminalde gördüğümüz validator_network_public_key
  
  
## Bu verileri doğru bir şekilde girdiğimize emin olduktan sonra `Validate Node` butonuna tıklayalım. Ardından eğer node'unuz Aptos takımı tarafından seçilirse mail alacaksınız ve sizden KYC istenecek. Bu yüzden süreç boyunca mail'lerinizi sık sık kontrol etmelisiniz.

# Kurulum bu kadardı, validatör olarak kullanabileceğiniz bazı komutları aşağıya bırakıyorum. Ayrıca optional olarak Fullnode yüklemek isterseniz [Aptos Fullnode Kurulumu](https://github.com/thisislexar/Aptos-AIT-3/blob/main/fullnode.md)'na göz atabilirsiniz. 


# Logları kontrol etmek için kod:

```
docker logs -f testnet-validator-1 --tail 50
```

# Senkronize durumunu kontrol etmek için kod:

```
curl 127.0.0.1:9101/metrics 2> /dev/null | grep aptos_state_sync_version | grep type
```
  
# Node'u tekrar başlatmak için kod:
```
docker restart testnet-validator-1
```  
  

