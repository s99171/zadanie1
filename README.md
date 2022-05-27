# Zadanie 1 Sprawozdanie - Justyna Baran

#### 1. Proszę napisać program serwera (dowolny język programowania), który realizować będzie następującą funkcjonalność:
#### a. po uruchomieniu kontenera, serwer pozostawia w logach informację o dacie uruchomienia, imieniu i nazwisku autora serwera (imię i nazwisko studenta) oraz porcie TCP,na którym serwer nasłuchuje na zgłoszenia klienta.
Kod:
![obraz](https://user-images.githubusercontent.com/105118113/170699469-a3e56707-514e-45bb-985b-11b3c31f0cbd.png)

Wynik:
![obraz](https://user-images.githubusercontent.com/105118113/170699680-ed744ed8-3640-4d06-961e-29ea80a3e365.png)

#### b. na podstawie adresu IP klienta łączącego się z serwerem, w przeglądarce powinna zostać wyświetlona strona informująca o adresie IP klienta i na podstawie tego adresu IP, o dacie i godzinie w jego strefie czasowej.
Kod:
![obraz](https://user-images.githubusercontent.com/105118113/170699528-ffa368de-356f-4319-a943-16f2d7340557.png)

Wynik:
![obraz](https://user-images.githubusercontent.com/105118113/170699808-baac8c25-7caf-4d80-93af-1a7cfab05bf6.png)

#### 2. Opracować plik Dockerfile, który pozwoli na zbudowanie obrazu kontenera realizującego funkcjonalność opisaną w punkcie 1.
Opracowany Dockerfile o nazwie: Dockerfile

#### 3. Należy podać polecenia niezbędne do:
##### a. zbudowania opracowanego obrazu kontenera:
`docker build -t zadanie1 .`

![obraz](https://user-images.githubusercontent.com/105118113/170701884-1ad10f79-59d4-498d-a10a-2a23f15ead93.png)
![obraz](https://user-images.githubusercontent.com/105118113/170701980-e2e78c24-0a8d-4e91-8693-4fffcf9b19e9.png)

##### b. uruchomienia kontenera na podstawie zbudowanego obrazu:
`docker run -it -d -p 8080:8080 zadanie1`

![obraz](https://user-images.githubusercontent.com/105118113/170702122-163d71fb-b0fc-4ed2-81b1-5d9c008dbe20.png)
![obraz](https://user-images.githubusercontent.com/105118113/170702269-49a04f62-aa7d-403b-a28f-22e796775a5e.png)

##### c. sposobu uzyskania informacji, które wygenerował serwer w trakcie uruchamiana kontenera:
`docker ps`

`docker logs 51484b8ffb00`
![obraz](https://user-images.githubusercontent.com/105118113/170702523-96c18cd5-da8e-41c0-9bef-f9d4740e3fd0.png)
![obraz](https://user-images.githubusercontent.com/105118113/170702615-5492e1f5-d8de-42a9-b6ee-fcbf7a950e7a.png)

##### d. sprawdzenia, ile warstw posiada zbudowany obraz:
`docker history zadanie1`
![obraz](https://user-images.githubusercontent.com/105118113/170702802-fda52dae-ce1f-4809-8c30-62fec2625127.png)

#### 3. Zbudować obrazy kontenera z aplikacją opracowaną w punkcie nr 1, które będą pracował na architekturach: linux/arm/v7, linux/arm64/v8 oraz linux/amd64. Obrazy te należy przesłać do swojego repozytorium na DockerHub.
1. Instalacja pakietu QEMU w lokalnym systemie plików:

`sudo apt-get install -y qemu-user-static`

![image5](https://user-images.githubusercontent.com/105118113/169279860-018aa83d-4a69-43dd-a67f-637cd0efe110.JPG)

2. Utworzenie środowiska budowania obrazów wykorzystującego wraper buildx

`docker buildx create --name testbuilder`

`docker buildx use testbuilder`

`docker buildx inspect --bootstrap`

![image6](https://user-images.githubusercontent.com/105118113/169280544-4a5065be-1834-4704-acbd-955eb4064b0f.JPG)

3. Obrazy dla trzech architektur sprzętowych: linux/amd64, linux/arm64/v8, linux/arm/v7 na podstawie Dockerfile za pomocą buildx oraz QEMU

`docker buildx build -t s99171/lab:z1 --platform=linux/amd64,linux/arm64/v8,linux/arm/v7 --push .`

![obraz](https://user-images.githubusercontent.com/105118113/170704794-1d78f867-2828-4a7e-914d-5bad16bc191b.png)

4. Weryfikacja parametrów utworzonych obrazów dla wybranych architektur sprzętowych

`docker buildx imagetools inspect s99171/lab:z1`
![obraz](https://user-images.githubusercontent.com/105118113/170704885-6602f949-bb56-43ec-a447-28e2278a4afd.png)

#### Część dodatkowa - Wykonać punkt 4 z wykorzystaniem GitHubActions 
Dodanie nazwy użytkownika i tokenu do DockerHub
![obraz](https://user-images.githubusercontent.com/105118113/170707384-aa3c4c6f-65b1-40af-9f85-19f8a6abc014.png)

Utworzenie pliku main.yml
![obraz](https://user-images.githubusercontent.com/105118113/170708055-13132c56-f07c-4ed1-a336-26c2c02a03ad.png)

Wynik:
![obraz](https://user-images.githubusercontent.com/105118113/170709656-302c65fb-d287-49f0-81a9-ad030903e677.png)

![obraz](https://user-images.githubusercontent.com/105118113/170709582-df482217-b0e1-4a82-a3ea-4482176d57d4.png)

