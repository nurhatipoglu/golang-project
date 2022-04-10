# golang-project
Golang kod örneği.

### Golang projesinin dockerize edilmesi.
Kod yazıldıktan sonra Dockerfile oluşturulur.

---

## Dockerfile Oluşturmak 
### From <base_image_adı:version>: 
+ Proje hangi kütüphanede yazıldıysa onun base image’ını belirttiğimiz kısımdır. Benim örnek projem go ile yazıldığı için _golang:1.16-alpine_** imagenı base almasını söyledim.

###  WORKDIR <klasör_yolu>:
+ Projemiz dosyalarını docker container’ın da hangi klasörün altına kopyalayacağını belirttiğimiz kısımdır. Projemizde _/app_** klasörünün altına kopyalarız.

### COPY <dosyalar> <kopyalanacak_klasör_yolu>: 
+ Belirtilen dosyaların belirtilen yere kopyalanmasını söylediğimiz kısımdır. Projede _ go.mod_** ve _go.sum_** dosyalarını kopyalarız. 
  
### RUN <komut>: 
+ Docker containerları hazırlanacağı sırada çalışması gereken komutlar için kullanılır. Projede go build -o /docker-gs-ping komutu çalıştırılır.
  
### EXPOSE <port_numarası>:
+ Oluşacak imaja ulaşmak için kullanılacak olan portun belirtildiği kısımdır. Projede _8080_** portu kullanılır. Proje ayağa kalktıktan sonra http://localhost:8080/ şeklinde sayfaya ulaşılabilir.
  
### CMD [<komutlar>]:
+ Docker containerında projemizin çalışması için kullandığımız komuttur. Bu komut docker run komutu çalıştırılırken düzenlenebilir.
  
---

### Image Build Etmek
sudo  docker build -t [image_name] .
  
### Image Run Etmek
sudo docker run -dp 8080:8080 [image_name] 
+ http://localhost:8080/ ile sayfa gelir.

### Çalışan Process leri Görmek
sudo docker ps 
+ container lar listelenir.

### Docker Hub a image i Push Etmek.
sudo docker push [image_name]
