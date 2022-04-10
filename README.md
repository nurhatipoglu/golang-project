# golang-project 
Golang kod örneği.
Inline-style: 
![alt text](https://tr.wikipedia.org/wiki/Go_(programlama_dili)#/media/Dosya:Go_Logo_Blue.svg "Logo Title Text 1")

### Golang projesinin dockerize edilmesi.
Kod yazıldıktan sonra Dockerfile oluşturulur.

---

## Dockerfile Oluşturmak 

```javascript
FROM golang:1.16-alpine

WORKDIR /app

COPY go.mod ./
COPY go.sum ./
RUN go mod download

COPY *.go ./

RUN go build -o /docker-gs-ping

EXPOSE 8080

CMD [ "/docker-gs-ping" ]
```


### From <base_image_adı:version>: 
+ Proje hangi kütüphanede yazıldıysa onun base image’ını belirttiğimiz kısımdır. Benim örnek projem go ile yazıldığı için **_golang:1.16-alpine_** imagenı base almasını söyledim.

###  WORKDIR <klasör_yolu>:
+ Projemiz dosyalarını docker container’ın da hangi klasörün altına kopyalayacağını belirttiğimiz kısımdır. Projemizde **_/app_** klasörünün altına kopyalarız.

### COPY <dosyalar> <kopyalanacak_klasör_yolu>: 
+ Belirtilen dosyaların belirtilen yere kopyalanmasını söylediğimiz kısımdır. Projede **_go.mod_** ve **_go.sum_** dosyalarını kopyalarız. 
  
### RUN <komut>: 
+ Docker containerları hazırlanacağı sırada çalışması gereken komutlar için kullanılır. Projede **_go build -o /docker-gs-ping_** komutu çalıştırılır.
  
### EXPOSE <port_numarası>:
+ Oluşacak imaja ulaşmak için kullanılacak olan portun belirtildiği kısımdır. Projede **_8080_** portu kullanılır. Proje ayağa kalktıktan sonra http://localhost:8080/ şeklinde sayfaya ulaşılabilir.
  
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
  
