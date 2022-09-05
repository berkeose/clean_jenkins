# clean_jenkins

# JENKINS NEDİR?
#### Jenkins basit tanım ile, bir yazılım projesinde dinamik olarak gerekli olan yapısal işlemleri otomatize ederek projeyi hızlı, kolaylıkla hata raporlaması ve kolay test edilip hataların fixlenebilmesini sağlayan bir CI(Continous Integration) aracıdır. 
#### Jenkins, Sürekli Entegrasyon (CI: Continuous Integration) yöntemi için kullanılan java ile yazılmış açık kaynak kodlu bir otomasyon sunucusudur. Yazılım geliştirme süreçlerini otomatize etmemize yarar. Jenkins, belirli bir sunucuda ve portta çalışır, belirlenen kaynaktan projeye ulaşır ve istenen işlemleri gerçekleştirir. Sonuçlarını belirlenen kişilere iletir. Bu sayede projemiz sürekli test edildiği için hatalar hızlıca tespit edilir ve çalışır bir vaziyette tutulur. Jenkins, manuel olarak yapılan build, test ve deploy gibi işlemleri uygular ve bu süreçte yaşanabilecek tüm aksaklık ve iletişim eksikliğini en aza indirir.

#### Kısacası Jenkins ‘Bu işlemlerle vakit kaybetmek istemiyorum, projemi kendi repona çek, oradaki istediğim test işlemlerini yap, ayağa kaldır, sonra deploy et. Bu işlemlerde fail eden bir durum olursa beni notification ile bilgilendir. Belirli aralıklarla github’ı da yokla. Bu yoklamalarda sana emrettiğim işlemleri tekrar et.’ gibi isteklerimizi yerine getiriyor. Bu noktada tüm bu işlemleri manuel olarak yaptığımız taktirde hem zaman hem hata riski hem de iş gücü sarfetmiş oluyoruz. Jenkins tüm süreçleri dikkatli ve müthiş bir şekilde basitleştirip otomatikleştiriyor.

## JENKINS NASIL ÇALIŞIR?
#### Jenkins, projemizi Git’ten çeker, build eder, yazılan test adımlarını belirlenen node’larda gerçekleştirir, sonuçlarını belirlenen kişilere iletir. Bunu sürekli hale getirir ve DevOps kültürünü oluşturur.
![1_S8C5nrFNzK1UJ-MJNKXFHQ](https://user-images.githubusercontent.com/81867200/187045350-de74b888-570a-4e28-833b-728b52bb9189.jpeg)

## JENKINS KAVRAMLARI
#### Job: Bir jenkins projesidir. Otomatize etmek istediğimiz işleri burada belirleriz. Örneğin, job config üzerinden şu repository’i çek, şu şartlarda build et, şu testleri çalıştır ve belirlenen kişilere mail at gibi işlemleri burada belirleriz.

#### Node: job’un üzerinde çalıştığı sunucuyu ifade eder. Testleri başka bir bilgisayarda koşmak istediğimizde node oluşturur ve bağlantı için gerekli şartları gerçekleştirdikten sonra node’da testlerimizi koşabiliriz.

#### Plugin (eklenti): Jenkins saf haliyle yüklenir, ihtiyacımıza göre plugin yükler ve bunları kullanılırız. Örneğin, Job çalıştıktan sonra mail atması için “Email Extension” eklentisini yüklemeli ve post-build adımında kullanmalıyız.

#### Pipeline: işlerin ardışık bir sırada yapılması, bir işlemin çıktısının sonraki gelen işlemin girdisi olması anlamına gelir. Ör: Bir test adımının başarısız olması durumunda diğer bir testin hiç başlamaması gibi. Fabrikadaki üretim bantlarını aklımıza getirelim. Üretilen eşya, hattın içerisinde farklı duraklara gelir. Her durakta bir işlem görür ve sonraki aşamaya geçer.

#### Stage: Pipeline içerisinde yer alan fazları ifade eder. Örneğin standart bir yazılım projesinde build -> test -> deploy adımlarından her birisi bir fazı ifade eder.

#### Step: Stage içerisinde yer alan adımları ifade eder.


#### Jenkins üzerinde kodumuzun geçtiği aşamaları düşünelim:

#### Build -> Test -> Deployment
#### Build (derleme) aşamasını bir evre (stage) olarak düşünelim. Test evresi de sonraki evre. Deployment evresi de en son çalışacak evre olarak düşünelim. Bu işlemler Jenkins üzerinde ardışık bir sırada çalışmaktadır.

#### Build işlemi hatalı olursa, yani kodumuz derlenmez ise, sonraki evreye geçmeyecektir. Aynı şekilde test safhasında hata oluşursa, deployment işlemi gerçekleşmeyecektir.

#### Pipeline mantığı bu şekilde çalışmaktadır.

## JENKINS'IN YAPISI
![piplen](https://user-images.githubusercontent.com/81867200/187047761-0bcf2f7f-62e1-4ac9-8c3c-baadcb2291b1.png)

### Her iş bir diğerini tetikler, eğer başarısız olan iş olursa tüm süreç başarısız olarak kesilir

## Continous Integration (Sürekli Entegrasyon)
#### Sürekli entegrasyon, geliştiricilerin yazdıkları yeni kodu kod tabanına günde en az bir kez ekleyerek geliştirme döngüsü boyunca daha sık entegre ettiği bir yazılım geliştirme sürecidir. Entegrasyon sorunlarını, düzeltmenin daha kolay olduğu daha erken dönemde belirlemek için derlemenin her yinelemesinde otomatikleştirilmiş test gerçekleştirilir. Bu, yayın için gerçekleştirilen son birleştirmede de sorunların önlenmesine yardımcı olur. Genel olarak sürekli entegrasyon, derleme sürecinin kolaylaştırılmasına yardımcı olur; bu da yazılım kalitesinin daha yüksek, teslimat zamanlamalarının daha öngörülebilir olmasını sağlar.

#### Sürekli entegrasyon (Continuous Integration = CI), kod üzerinde yapılan her değişikliğin ardından, tüm sistemin çalışır durumda olduğunu, yapılan değişikliğin sistemin bazı bölümlerinde kırılmalara yol açmadığını tespit etmek için kullanılan yöntemdir.
### Kırılmaları birim testlerle tespit ederiz. Bu testler, yapılan değişikliğin neticesi olarak yeni bir yapı (build) hazırlandıktan sonra otomatik olarak çalıştırılır.
#### Yapılan değişiklik yeni yapının bir parçası olduğu için, testlerde oluşan hatalar, yapılan değişikliğin sistemi kırdığı anlamına gelmektedir. Bu durumdan tüm programcılar haberdar edilerek, hatanın bir an önce giderilmesi ve testlerin her zaman olumlu sonuç vermesi sağlanır.
#### Sürekli entegrasyon ile programcılar tarafından kod üzerinde yapılan çalışmalar neticesinde her zaman çalışır bir sürümün oluşması sağlanmış olur.

### NEDEN SÜREKLİ ENTEGRE EDİLMELİ?
#### Şimdi şunu hayal edin: Yeni bir otomobilin tasarlanması projesinde yer aldınız. Otomobil tasarlandı ve otomobili oluşturan parçalar 5 değişik ülkede, 20 değişik firma tarafından üretildi. Bu ülkelerde kullanılan uzunluk ve ağırlık birimleri (metre, kg vs.) değişik olabilir. Görev dağılımı esnasında yanlış anlamalardan dolayı üretilen parçalar birbirine uyumlu olmayabilir. Eğer tüm parçalar üretildikten sonra bir çırpıda tüm otomobili oluşturmak isterseniz, üretim sürecinde meydana gelen hataları daha önceden tespit edemediğiniz için, yamuk yumuk bir otomobil ortaya çıkacaktır. Ama üretim esnasında koordineli bir şekilde otomobili parça parça bir araya getirip, parçalar uyuşuyor mu diye kontrol etmiş olsaydınız, meydana gelen uyuşmazlıkları çok erken tespit ederek, gerekli değişiklikleri yapabilirdiniz. Bu yazılım sektörü için de geçerli.  Oluşturulan sistem komponentleri ne kadar erken entegre edilirse, oluşan uyuşmazlıklar o kadar erken tespit edilir ve gerekli değişiklikler yapılabilir.

#### Sürekli entegrasyon çevik süreçlerde çok önemli bir yazılım metodudur. Sistem üzerinde yapılan her değişiklik sürekli entegrasyonu otomatik olarak gerçekleştiren sunucu tarafından kontrol edilir.  Yazılımda kırılmalar oluşması (compile hataları, eksik sınıflar vs.) durumunda, tüm ekip sürekli entegrasyon sunucusu tarafından uyarılır. Bu geribildirim sayesinde entegrasyonun ne safhada olduğu anlaşılır.

## CONTINOUS TESTING
#### Derlenmiş kodun üstünde entegrasyon, fonksiyonel vb. testlerin geçirildiği ve koda güvenin sağlandığı süreçtir.

### NEDEN CONTINOUS TESTING
#### Çevikleşen yazılım dünyasının omurgasını oluşturan sürekli geri bildirim yaklaşımına hayat veren “Continuous Testing”; daha hızlı, hatasız ve kapsamlı test aktiviteleri ile bir araya getirilen yazılım parçalarının sorunsuz çalıştığından emin olmayı sağlar.
### Continuous Testing, DevOps dönüşümünün en önemli ve ilk adımlarındandır. Kurumsal çevikliğin sağlanmasında önemli bir mühendislik aşaması ve ürüne yeni eklenen özelliklerin mevcut fonksiyonaliteyi bozmadığının garantisidir.

![ct](https://user-images.githubusercontent.com/81867200/187047623-617e5ade-e0a2-4cd8-a1e7-694485c1bb5f.png)

## Continous Delivery (Sürekli Teslim)
#### Sürekli teslim, ekiplerin kısa döngüler halinde yazılım ürettiği, yazılımın herhangi bir zamanda ve yazılımı serbest bırakırken manuel olarak yapmadan güvenilir bir şekilde yayınlanabilmesini sağlayan bir yazılım mühendisliği yaklaşımıdır.

#### Kısaca Sürekli Teslimat(CD),deploy etmek zorunda olmadığın ama her zaman buna hazır olduğun andır.

### Continus Delivery aşağıdaki üç disiplinin kombinasyonu demektir.
#### - Continuous Integration
#### - Continuous Testing
#### - Continuous Deployment (istendiğinde)

### HEDEFLER
#### -Kullanıcıya çalışan yazılımı olabildiğince hızlı verebilmek
#### -Sıklıkla otomatize edilmiş sürümler sunmak

### FAYDALAR
#### Düşük risk, stres
#### -Hızlı yatırımın geri dönüşü (ROI)
#### -İş ihtiyaçlarına geliştirilmiş yanıt verebilmek
#### -İyileştirilmiş kalite
#### -Hızlıca hataya düşmek (fail-fast)
#### -Yüksek özgüven

### JENKINS'İN ETKİLEŞİMLERİ
![133](https://user-images.githubusercontent.com/81867200/187045617-a2fb7581-611c-4064-b974-3098c7c72163.jpg)

### JENKINS İÇİNDE KULLANILAN TEKNOLOJİLER
![JENKİNSİÇİ](https://user-images.githubusercontent.com/81867200/187048107-bf8e9a60-cc46-4223-bc59-161a57335c8e.png)

## JENKINS MİMARİSİ
#### - Jenkins, her yazılım gibi bir işletim sistemi(host) üstünde koşar.
#### - Java application container veya application server üstünde koşar (varsayılan olarak Jetty kullanır)
#### - Jetty ve jenkinsi başlatma, durdurma ve izlemek için harici bir servis uygulaması çalışır.
#### - Views ile projeleri(jobs olarak da bilinir) ve klasörleri gruplar Jenkins.
#### - Projeler iş kuyruklarını (job queue) ve bunları çalıştıracak executerları tetikler.
![arcj](https://user-images.githubusercontent.com/81867200/187048310-fd148097-fdbc-42a6-80b8-7c65dc7f3261.png)


![1](https://user-images.githubusercontent.com/81867200/187048401-cc0ebb49-4845-47b7-a87f-6f004b5035e9.png)


### İlk olarak bir job yaratmak için bir Job ismi belirtip nasıl yapılandıracağımızı seçiyoruz.
![1](https://user-images.githubusercontent.com/81867200/185698209-2a3b7742-bf35-4808-b705-e02707e11958.png)
### WORKSPACES
![2](https://user-images.githubusercontent.com/81867200/187048560-60ee566d-0254-4c76-b29b-9d0e115c707a.png)

### DİZİN LAKAPLARI
![3](https://user-images.githubusercontent.com/81867200/187048943-e2d8c726-dfd3-4bdb-aa48-7f858de7c1b6.png)

### PROJE-JOB YAPILANDIRMA DURUMLARI
![4](https://user-images.githubusercontent.com/81867200/187048996-79a4849d-2525-4839-a052-8cbc848dbd5c.png)

## PIPELINE NASIL TANIMLANIR?
#### Jenkins Pipeline tanımı JenkinsFile isminde bir dosyaya yazılır.

#### İki türlü tanımlama şekli var: Declarative, Scripted

#### Bu iki tür pipeline yazım şeklinden declarative olanı sonradan gelmiş ve daha gelişmiş olanıdır.
#### Resmi Jenkins dokümanlarında tavsiye edilen yöntem declarative tanımlamadır.
#### Scripted tanımlamada groovy kullanılarak yapılır. Declarative tanımlama tavsiye edilmesine rağmen, scripted tanımlama ile herhangi bir kısıtlama olmadan herşeyi yapabiliyorsunuz.
#### Scripted tanımlama bize daha esnek bir tanımlama imkanı sunuyor. İkisini de tercih edebilirsiniz.

#### DECLARATIVE VS SCRIPTED
#### Deklaratif ardışık düzen ile Komutlu ardışık düzen arasındaki temel fark, sözdizimleri ve esneklikleriyle ilgilidir.

#### Deklaratif pipeline, pipeline’ı kod konsepti olarak destekleyen nispeten yeni bir özelliktir. Pipeline kodunun okunmasını ve yazılmasını kolaylaştırır. Bu kod Git gibi bir kaynak kontrol yönetim sistemine kontrol edilebilen bir Jenkinsfile içinde yazılmıştır.

#### Oysa (Scripted) kodlanmış pipeline, kodu yazmanın geleneksel bir yoludur. Bu satırda Jenkinsfile Jenkins UI örneğine yazılır. 
#### Bu boru hatlarının her ikisi de Groovy DSL'ye dayanmasına rağmen, scripted pipeline, Groovy tabanlı daha katı sözdizimleri kullanır çünkü Groovy üzerine inşa edilen ilk pipeline idi. 

#### Bu Groovy komut dosyası genellikle kullanıcılar tarafından benimsenmediğinden, daha basit ve daha seçenekli bir Groovy sözdizimi sunmak için deklaratif ardışık düzen eklendi.

#### Deklaratif (bildirimli) ardışık düzen, "pipeline" etiketli bir blok içinde tanımlanırken, komut dosyası verilen ardışık düzen, bir "node" içinde tanımlanır.

### SCRIPTED
#### Scripted pipeline, Jenkins pipeline’ı kod olarak yazmanın geleneksel bir yoludur. İdeal olarak, Scripted pipeline Jenkins web arayüzünde Jenkins dosyasında yazılır. 

#### Deklaratif düzenden farklı olarak, scripted pipeline katı bir sözdizimi kullanır. Bu nedenle, scripted pipeline kodlanmış pipeline üzerinde büyük denetim sağlar ve komut dosyasının akışını kapsamlı bir şekilde değiştirebilir.
#### Bu, geliştiricilerin kod olarak ileri ve karmaşık boru hattı geliştirmelerine yardımcı olur.

![5](https://user-images.githubusercontent.com/81867200/187049274-0abd17c4-3b2f-4307-9772-97fb8c4f35ee.png)
#### Node, Jenkins mimarisinin, node veya agent projelerin iş yükünün bir kısmını çalıştıracağı ve ana düğümün (master node) işin yapılandırmasını (configuration) işleyeceği kısmıdır.
#### Stage bloğu görev ilerledikçe tek bir aşama veya çoklu olabilir. Ve ortak aşamaları olabilir.




