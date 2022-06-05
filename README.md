# projects

Springboot Hello world projesi için ;

ihtiyacımız olan araçlar
Docker
Kubernetes
Maven

Öncelikle hello world metnini içeren app.java 'ya ve hello controller'a ihtiyacımız var hello controller'ı hello world metnini döndürmek için kullanıyoruz.. 
Gerekli paketleri yükleyebilmek için "pom.xml" dosyamı maven ile build alıyorum. Gerekli maven sürümlerini Dockerfile dosyamda vardır. Direk dockerfile dosyasını build almanız yeterlidir.

Kubernetes'e manuel Deploy Etmek için ;

Öncelikle imajları pushlayıp kubernetes'e çekebilmek için private veya public registry'ê ihtiyacımız vardır.

Values.yaml Dosyasında Deployment ve Service vardır. Kendi sistemimize göre revize ediyoruz. Deployment'ta bulunan Containers'a Repomuzun bilgilerini veriyoruz.
Ben Docker Hub'a pushladım.

Namespace oluşturuyoruz.

kubectl create ns deneme-hello

kubectl appyl -f values.yaml --namespace=deneme-hello


Projeye DNS üzerinden ulaşabilmek için nginx-ingress aracılığıyla dışarıya yönlendiriyorum. Şu an http olarak yayınlandı fakat istersek elimizdeki sertifikalar
ile tls secret oluşturup ingress.yaml'da belirtip https olarak dışarıya açmış oluruz. Elimde DNS adresi olmadığı için Host'a sahte dns veriyorum.

kubectl apply -f ingress.yaml --namespace=deneme-hello
