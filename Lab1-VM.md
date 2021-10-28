# [Compute Engine](https://cloud.google.com/compute) - [Virtual Machine](https://cloud.google.com/learn/what-is-a-virtual-machine)
Podstawy deployowania VM w GCP:
1. Regiony i Strefy
2. Rodzaje VM'ek
3. Deployowanie VM z UI
4. Deployowanie VM z Cloud Shell

# Podstawy deployowania VM w GCP
## 1 [Regiony i strefy](https://cloud.google.com/about/locations/#regions):
Niektóre zasoby Compute Engine znajdują się w regionach lub strefach. Region to określona lokalizacja geograficzna, w której możesz uruchomić swoje zasoby. Każdy region zawiera co najmniej 1 strefę. Na przykład us-central1 to region w środkowych Stanach Zjednoczonych zawierający strefy `us-central1-a`, `us-central1-b`, `us-central1-c` i `us-central1-f`. Warszawa to `europe-central2`.

![available zones](https://cdn.networkmanagementsoftware.com/wp-content/uploads/gcp-regions-and-zones-1024x362.png)

Zasoby znajdujące się w strefach są nazywane zasobami strefowymi. W strefie znajdują się instancje maszyny wirtualnej i dyski stałe. Aby można było podłączyć dysk stały do instancji maszyny wirtualnej, oba zasoby muszą znajdować się w tej samej strefie. Analogicznie: aby możliwe było przypisanie do instancji statycznego adresu IP, musi się ona znajdować w tym samym regionie co statyczny adres IP.

## 2. [Rodzaje VM'ek i opłaty](https://cloud.google.com/compute/all-pricing)
Compute Engine pobiera opłaty za użytkowanie na podstawie poniższego cennika. Rachunek jest wysyłany na koniec każdego cyklu rozliczeniowego, wymieniając poprzednie użycie i opłaty. Ceny na tej stronie są podane w dolarach amerykańskich (USD).

W przypadku Compute Engine rozmiar dysku, pamięć typu maszyny i użycie sieci są obliczane w gigabajtach (GB), gdzie 1 GB to 230 bajtów.

Jeśli płacisz w walucie innej niż USD, obowiązują ceny podane w Twojej walucie w jednostkach [SKU Cloud Platform](https://cloud.google.com/skus/).

You can also find pricing information with the following options:

-   Zobacz szacunkowe koszty swoich instancji i zasobów Compute Engine podczas ich tworzenia w  [Google Cloud Console](https://console.cloud.google.com/).
-   Oszacuj całkowite koszty projektu za pomocą  [Google Cloud Pricing Calculator](https://cloud.google.com/products/calculator).
-  Przeglądaj i pobieraj ceny z  [Pricing Table](https://cloud.google.com/billing/docs/how-to/pricing-table)  w Cloud Console.
-   Użyj rozliczeń w chmurze  [Catalog API](https://cloud.google.com/billing/v1/how-tos/catalog-api)  for programmatic access to  [SKU](https://cloud.google.com/skus)  information.

## 3. Deployowanie VM z UI
## 4. Deployowanie VM z Cloud Shell
Podstawowe polecenie zdeployowania VM'ki.
```shell
gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone europe-central2
```
**Szczegóły polecenia**

-   Parametr  `gcloud compute`  pozwala zarządzać zasobami Compute Engine w prostszym formacie niż Compute Engine API.
    
-   Parametr  `instances create`  tworzy nową instancję.
Można sprawdzać ustawienia domyśle (lub czy są one w ogóle ustawione)
-   Parametr  `gcelab2`  zawiera nazwę nowej maszyny wirtualnej.
    
-   Flaga  `--machine-type`  pozwala określić typ maszyny jako  _n1-standard-2_.
    
-   Flaga  `--zone`  pozwala określić miejsce utworzenia maszyny wirtualnej.
	-   Pominięcie flagi  `--zone`  spowoduje, że  `gcloud`  ustawi wybraną strefę na podstawie właściwości domyślnych. Jeśli w poleceniu  `create`  nie podasz pozostałych wymaganych ustawień instancji, takich jak  `machine type`  (typ maszyny) i `image`  (obraz), zostaną ustawione wartości domyślne.

Ustawienia domyśle:
```shell
gcloud config get-value compute/zone
gcloud config get-value compute/region
```
powyższe komendy zwracają domyślne ustawienia strefy oraz regionu. Jeśli otrzymujemy `unset`, znaczy że nie ma ustawionej domyślnej wartości

Wygodnie jest używać zmiennych środowiskowych w celu uproszczenia poleceń oraz dla porządku.

Zmienna środowiskowa do przechowywania ID projektu (ID oznaczamy jako `<ID_projektu>`)  oraz druga strefy
```shell
export PROJECT_ID=<ID_projektu>
export ZONE=<strefa>
```
Żeby sprawdzić poprawność wartości zmiennych wpisujemy 
```shell
echo $PROJECT_ID
echo $ZONE
``` 
Podstawowa komenda do tworzenia VM'ki wygląda teraz tak (zmienia się tylko zmienna strefy)
```shell
gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone $ZONE
```
