# HuDeX Api

## Ön adımlar
1. Ganache kurulumu
2. Kontratlar klasöründeki kontratların Remix IDE kullanılarak Ganache'da oluşturulmuş çalışma alanına deploy edilmesi
   
   1. Kontratların Remix IDE'ye yüklenmesi
        
        ![alt text](kontrat_yukle.png)
   
   2. Gerekli Pluginlerin aktifleştirilmesi
   
        ![alt text](aktiflestirilecek_pluginler.png)
   
   3. Derlenecek kontratın seçilmesi
   
        ![alt text](deploy_edilecek_kontrat.png)
   
   4. Kontratın derlenmesi
   
        ![alt text](compile_etme.png)
   
   5. Environment Seçimi
   
        ![alt text](env_secimi.png)
   
   6. Environment rpc adresinin ayarlanması
   
        ![alt text](rpc_adresi.png)
   
   7. Deploy ayarlarının yapılması ve deploy
   
        ![alt text](deploy_ayarları.png)
   
   8. Kontrat adresinin öğrenilmesi
   
        ![alt text](kontrat_adresinin_alinmasi.png)
   


3. index.js dosyasındaki kontrat adresinin değiştirilmesi (Kontrat abi'si index.js içerisine önceden eklenmiştir.)
   ```js
   var erc1155 = new web3.eth.Contract(<CONTRACT_ABI>, <CONTRACT_ADDRESS>)
   ```

4. Kullanılacak proje dizininde ``` npm install <../PATH/TO/HUDEX/API> ``` komutu ile kütüphanenin projeye eklenmesi

## Kullanım

```js
var HuDeX = require('hudex_api');

var hudex = new Hudex.HuDeX(<DEVELOPER_ETH_ADDRESS>, <DEVELOPER_ID>, <GAME_ID>)
```

DEVELOPER_ID: Geliştiricinin HuDeX borsasındaki kullanıcı id'si

GAME_ID: Oyunun HuDeX borsasındaki id'si


## Komutlar

1. balanceOf
   
    Parametreler:

        usr_addr: Bakiyesi öğrenmek istenilen kullanıcının eth adresi
        token_id: Bakitesi öğrenmek istenilen tokenın idsi

    Fonksiyonun Cevabı:
        
        Promise içerisinde {<token_id>: <bal:int>} objesini çevirir.

2. balanceOfBatch
   
    Parametreler:

        usr_addr: Bakiyesi öğrenmek istenilen kullanıcının eth adresi
        token_id: Bakitesi öğrenmek istenilen tokenların idleri

    Fonksiyonun Cevabı:
        
        Promise içerisinde {<token_id>: <bal:int>} ikililerini içeren obje çevirir.

3. createAndMint
   
    **Parametreler:**

        createArgs: hudex kütüphanesinde bulunan CreateArgs objesidir. Objenin oluşturucusu sırayla name (string. tokenın adı), is_nf (bool. true:Non-Fungible; false:Fungible), quantity (int. Üretilecek miktar. Non-Fungible için gereksiz.) ve img (string. Token resminin bulunduğu path veya internet adresi.) parametrelerini alır.

    Fonksiyonun Cevabı:
        
        Promise içerisinde {tokenId: <Olusturulan_tokenın_idsi>, mint: <basarim:bool>} objesini döner. Üretim başarılı ise mint değeri true, değil ise false olarak gönderilir.

4. mint (Sadece Fungible tokenlar için)
   
    Parametreler:

        tokenId: Üretilmek istenen tokenın idsi.
        quantity: Kaç tane üretilmek istendiği.

    Fonksiyonun Cevabı:
        
        Promise içerisinde {tokenId: <Olusturulan_tokenın_idsi>, mint: <basarim:bool>} objesini döner. Üretim başarılı ise mint değeri true, değil ise false olarak gönderilir.

5. transfer
   
    Parametreler:

        senderAddr: Gönderenin eth adresi.
        toAddr: Alıcının eth adresi.
        tokenId: Transfer edilmek istenilen tokenın idsi
        quantity: Ne kadar gönderilmek istendiği.


    Fonksiyonun Cevabı:
        
        Promise içerisinde {transfer: <bool>} objesini döner.

1. burn
   
    Parametreler:

        senderAddr: Tokenı yakılacak kişinin eth adresi.
        tokenId: Yakılmak istenilen tokenın idsi
        quantity: Ne kadar yakılmak istendiği.

    Fonksiyonun Cevabı:
        
        Promise içerisinde {transfer: <bool>} objesini döner.

2. ownerOf
   
    Parametreler:

        tokenId: Sahibi öğrenilmek istenen Non-Fungible token idsi

    Fonksiyonun Cevabı:
        
        Promise içerisinde sahibinin adresini döner.

3. ownedBy
   
    Parametreler:

        addr: Kullanıcı adresi

    Fonksiyonun Cevabı:
        
        Promise içerisinde <addr> adresinin sahip olduğu tokenların idlerinin listesini döner.
