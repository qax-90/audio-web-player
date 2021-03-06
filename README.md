# Audio Web Player wersja 4
**Audio Web Player** to prosty odtwarzacz plików muzycznych MP3, który w prosty sposób każdy może dodać do swojej strony internetowej zupełnie za darmo. Stawiając nacisk na jego prostotę, posiada intuicyjny w obsłudze interfejs, który umożliwia łatwą zmianę aktualanie odtwarzanego utworu za pomocą przycisków nawigacyjnych oraz za pomocą dowolnej ułożonej przez użytkownika listy odtwarzania. Aplikacja w czasie rzeczywistym wyświetla postęp odtwarzanego utworu, który można w prosty sposób przewinąć do dowolnego miejsca klikając pasek postępu. Ponadto program nie tylko wyświetla informacje o nazwach wykonawców, tytułów utworów, albumów oraz lat ich wydania, ale pozwala na dodawanie okładek albumów w tym ich odpowiedników o wysokiej rozdzielczości, które są powiększane po kliknięciu miniaturki.

## Historia zmian
Wersja 2: W drugiej odsłonie aplikacji dodano pokrętło do regulacji głośności; możliwość dostosowania interfejsu użytkownika (m.in. etykiet tekstowych, w tym formatu wyświetlanego czasu utworu); wprowadzono również motyw o ciemnej kolorystyce, który obecnie jest domyślny (oczywiście, istnieje możliwość powrotu do starej jasnej szaty graficznej).

Wersja 3: W trzeciej wersji programu wprowadzono większą kontrolę nad formą przedstawianych informacji w liście odtwarzania, a także dodano możliwość jej wyłączenia według własnych preferencji; zrezygnowano z konieczności wypełniania wszystkich danych o utworach (teraz jedyne wymagane pole to nazwa pliku dźwiękowego); ponadto naprawiono problem związany z regulacją głośności za pomocą pokrętła.

Wersja 4: Wraz z ukazaniem się czwartej wersji aplikacji, odtwarzacz stał się bardzo przyjazny w obsłudze przez osoby niepełnosprawne (zastosowano WAI-ARIA); w pliku konfiguracyjnym dodano opcję włączenia, bądź wyłączenia automatycznego odtwarzania kolejnych utworów według kolejności w playliście; dodatkowo poprawiono wyświetlanie interfejsu użytkownika na małych ekranach urządzeń (zastosowano RWD).

## Instrukcja instalacji
1. Pierwszą czynnością jest skopiowanie katalogu *awp* do katalogu z własną stroną internetową, na której ma być zamieszczony Audio Web Player.

2. Wszystkie pliki muzyczne MP3 należy skopiować do katalogu *awp/tracks/* pod dowolną nazwą. Aplikacja domyślnie zawiera trzy przykładowe utwory w formacie MP3 @ 192kb/s, które należy skasować, bądź zamienić na inne.

3. Wszystkie pliki graficzne z okładkami albumów należy skopiować do katalogu *awp/covers/* pod dowolną nazwą. Zaleca się wykorzystanie obrazów wysokiej rozdzielczości (na przykład 1000 pikseli na 1000 pikseli), aby uniknąć efektu rozmycia przy ich powiększaniu.

4. Wszystkie pliki graficzne z miniaturami okładek albumów należy skopiować do katalogu *awp/thumbnails/*, każdy pod identyczną nazwą i rozszerzeniem jak w katalogu wymienionym powyżej (czyli w tym katalogu z okładkami wysokiej rozdzielczości). Zaleca się wykorzystanie obrazów niższej rozdzielczości (na przykład 300 pikseli na 300 pikseli) oraz silniejszej kompresji, aby zapobiec opóźnieniom w ich wczytywaniu przy zmianie odtwarzanego utworu.

5. Kolejnym krokiem jest dodanie arkusza stylów CSS (podając właściwą ścieżkę do tego pliku) oraz pliku skryptu JavaScript (również podając właściwą ścieżkę do tego pliku) wewnątrz sekcji `<head>` i `</head>` na stronie, na której ma zostać umieszczony Audio Web Player, wklejając poniższy kod HTML, na przykład:
      ```
      <link href="awp/sources/awp.min.css" rel="stylesheet" />
      <link href="awp/sources/awp-light-theme.min.css" rel="stylesheet" title="Jasny motyw" />
      <link href="awp/sources/awp-dark-theme.min.css" rel="stylesheet" title="Ciemny motyw" disabled />
      <script src="awp/sources/awp.min.js"></script>
      ```

      Wskazówka: W powyższym kodzie włączono jasny motyw poprzez dodanie atrybutu `disabled` do importowanego arkusza styli z ciemnym motywem. W razie chęci włączenia ciemnej kolorystyki, należy przenieść ten atrybut do tego pierwszego.

6. Następnie należy dodać informacje o ustawieniach interfejsu odtwarzacza oraz o liście utworów wyświetlanych w odtwarzaczu. Dane te są przechowywane w pliku *awp/sources/settings.json*. Obowiązuje w nim zapis w formacie JSON dzielącego się na obiekt *interface* (którego nie ma konieczności zmieniać) oraz *playlist* składającego się z tablicy obiektów (w poniższym przykładzie zamieszczono trzy utwory), na przykład:
      ```
       {
        "interface": {
          "headerTitle": "Odtwarzacz muzyki",
          "trackTitleStopped": "Tytuł utworu",
          "artistNameStopped": "Nazwa artysty",
          "coverImageTitle": "Okładka albumu",
          "playlistHeaderSubtitle": "Kliknij poniżej wybrany utwór, aby rozpocząć jego odtwarzanie:",
          "showPlaylist": true,
          "playlistContinuous": true,
          "showPreviousButton": true,
          "showNextButton": true,
          "showStopButton": true,
          "showVolumeKnob": true,
          "setVolumeOfSound": "full",
          "timeFormat": "$cur_min_1$:$cur_sec_2$ / $dur_min_1$:$dur_sec_2$",
          "playlistItemTitleFormat": "$artist_name$ – $track_name$ [$dur_min_1$:$dur_sec_2$]",
          "playlistItemSubtitleFormat": "z albumu $album_name$ z roku $release_year$",
          "selectedTrack": "none",
          "waiAriaStartTabIndex": "auto"
        },
        "playlist": [
          {
            "artistName": "Shpongle",
            "trackName": "Divine Moments Of Truth",
            "albumName": "Are You Shpongled?",
            "releaseYear": "1998",
            "coverFile": "shpongle-are-you-shpongled.jpg",
            "trackFile": "shpongle-divine-moments-of-truth.mp3",
            "durationTimeMinutes": 10,
            "durationTimeSeconds": 20
          },
          {
            "artistName": "Infected Mushroom",
            "trackName": "Heavyweight",
            "albumName": "Vicious Delicious",
            "releaseYear": "2007",
            "coverFile": "infected-mushroom-vicious-delicious.jpg",
            "trackFile": "infected-mushroom-heavyweight.mp3",
            "durationTimeMinutes": 8,
            "durationTimeSeconds": 41
          },
          {
            "artistName": "Younger Brother",
            "trackName": "All I Want",
            "albumName": "The Last Days Of Gravity",
            "releaseYear": "2007",
            "coverFile": "younger-brother-the-last-days-of-gravity.jpg",
            "trackFile": "younger-brother-all-i-want.mp3",
            "durationTimeMinutes": 9,
            "durationTimeSeconds": 4
          }
        ]
      }
      ```
7. Obiekt *interface* reprezentujący strukturę interfejsu aplikacji obowiązkowo musi składać się z 17 następujących pól wraz z przypisanymi wartościami:
     - *"headerTitle":* – dowolny tytuł aplikacji
     - *"trackTitleStopped":* – dowolny tekst wyświetlany w miejscu tytułu utworu, gdy odtwarzanie jest zatrzymane
     - *"artistNameStopped":* – dowolny tekst wyświetlany w miejscu nazwy artysty, gdy odtwarzanie jest zatrzymane
     - *"coverImageTitle":* – dowolny tekst dodawany przed nazwą okładki albumu
     - *"playlistHeaderSubtitle":* – dowolny tekst wyświetlany przed listą odtwarzania
     - *"showPlaylist":* – ustawić *true* jeśli lista odtwarzania ma być wyświetlana lub *false* w przeciwnym wypadku
     - *"playlistContinuous":* – ustawić *true* jeśli odtwarzanie kolejnych utworów ma przebiegać automatycznie lub *false* w przeciwnym wypadku
     - *"showPreviousButton":* – ustawić *true* jeśli przycisk zmiany utworu na poprzedni ma być wyświetlany lub *false* w przeciwnym wypadku
     - *"showNextButton":* – ustawić *true* jeśli przycisk zmiany utworu na następny ma być wyświetlany lub *false* w przeciwnym wypadku
     - *"showStopButton":* – ustawić *true* jeśli przycisk zatrzymania odtwarzania utworu ma być wyświetlany lub false w przeciwnym wypadku
     - "showVolumeKnob": – ustawić true jeśli pokrętło zmiany poziomu głośności ma być wyświetlane lub *false* w przeciwnym wypadku
     - *"setVolumeOfSound":* – poziom poziomu głośności po uruchomieniu aplikacji ustawianej z zakresu od *0* do *100* (sama liczba bez innych dodakowych znaków), wpisanie *"full"* oznacza pełną głośność (jest to domyślne ustawienie)
     - *"timeFormat":* – określa format wyświetlanego formatu aktualnego czasu zamieniając zmienne ujęte pomiędzy znakami dolarów na rzczywiste wartości; poniżej przedstawiono przykładowe prawidłowe zapisy wartości pola *"timeFormat":*:
          - *"$cur_min_1$:$cur_sec_2$ / $dur_min_1$:$dur_sec_2$"* – wyświetla czas w formacie: 0:00 / 0:00
          - *"$cur_min_2$:$cur_sec_2$ / $dur_min_2$:$dur_sec_2$"* – wyświetla czas w formacie: 00:00 / 00:00
          - *"upłynęło $cur_min_1$ minut i $dur_sec_1$ sekund"* – wyświetla czas w formacie: upłynęło 0 minut i 0 sekund
          - *"czas trwania: $dur_min_1$ min. i $dur_sec_2$ sek."* – wyświetla czas w formacie: czas trwania: 0 min. i 00 sek.
          - *"$full_cur_sec_1$ sek. z $full_dur_sec_3$ sek."* – wyświetla czas w formacie: 0 sek. z 000 sek.
     - *"playlistItemTitleFormat":* – określa format wyświetlanego formatu tytułu każdej pozycji w liście odtwarzania, zamieniając zmienne ujęte pomiędzy znakami dolarów na rzczywiste wartości; poniżej przedstawiono przykładowe prawidłowe zapisy wartości pola *"playlistItemTitleFormat":*:
          - *"$track_name$ o czasie trwania $dur_min_1$ min. i $dur_sec_1$ sek."* – wyświetla tytuł każdej pozycji w formacie: Nazwa utworu o czasie trwania 0 min. i 0 sek.
          - *"$artist_name$ – $track_name$ [$dur_min_1$:$dur_sec_2$]"* – wyświetla tytuł każdej pozycji w formacie: Nazwa artysty – Nazwa utworu [0:00]
          - *"utwór $track_name$ w wykonaniu $artist_name$ o długości $full_dur_sec_3$ sek."* – wyświetla tytuł każdej pozycji w formacie: utwór Tytuł utworu w wykonaniu Nazwa artysty o długości 000 sek.
     - *"playlistItemSubtitleFormat":* – określa format wyświetlanego formatu podtytułu każdej pozycji w liście odtwarzania, zamieniając zmienne ujęte pomiędzy znakami dolarów na rzczywiste wartości; poniżej przedstawiono przykładowe prawidłowe zapisy wartości pola *"playlistItemSubtitleFormat":*:
          - *"z albumu $album_name$ z roku $release_year$"* – wyświetla podtytuł każdej pozycji w formacie: z albumu  Nazwa albumu z roku 0000
          - *"z albumu $album_name$ w wykonaniu $artist_name$"* – wyświetla podtytuł każdej pozycji w formacie: z albumu  Nazwa albumu w wykonaniu Nazwa artysty
     - *"selectedTrack":* – numer domyślnie wczytywanego i wybieranego utworu z listy odtwarzania po uruchomieniu aplikacji (*1* oznacza pierwszy utwór, *3* to trzeci utwór, itd.), wpisanie *"none"* oznacza, że żaden utwór nie zostanie wstępnie wczytany i wybrany (jest to domyślne ustawienie)
     - *"waiAriaStartTabIndex":* – numer od jakiego ma zostać rozpoczęte przypisywanie wartości atrybutom *tabindex* elementom nawigacyjnym programu według zasad WAI-ARIA (wpisanie *auto* oznacza rozpoczęcie od kolejnego po ostatnim numerze elementu nawigacyjnym całej strony internetowej i jest to domyślne ustawienie)

8. Każdy obiekt z tablicy obiektów playlist reprezentujący poszczególny utwór z listy odtwarzania powinien (choć nie musi) składać się z 8 następujących pól wraz z przypisanymi wartościami:
     - *"artistName":* – nazwa artysty utworu
     - *"trackName":* – nazwa utworu
     - *"albumName":* – nazwa albumu z którego pochodzi utwór
     - *"releaseYear":* – rok wydania albumu
     - *"coverFile":* – pełna nazwa pliku okładki albumu (zarówno miniaturki jak i obrazu w wysokiej rozdzielczości)
     - *"trackFile":* – pełna nazwa pliku utworu (pole obowiązkowe)
     - *"durationTimeMinutes":* – liczba określająca długość czasu trwania utworu w minutach
     - *"durationTimeSeconds":* – liczba określająca długość czasu trwania utworu w sekundach (reszta z czasu trwania w minutach)

9. Na końcu możliwe jest umieszczenie aplikacji Audio Web Player na własnej stronie internetowej. W tym celu należy wkleić krótki poniższy kod HTML, dokładnie w tym miejscu, gdzie ma się wyświetlić odtwarzacz:
      ```
      <div id="audio-web-player"></div>
      ```
      Wskazówka: Nie jest możliwe uruchomienie aplikacji lokalnie na komputerze – konieczne jest umieszczenie jej na serwerze WWW!

10. Opcjonalnie, odtwarzacz można dowolnie dostosowywać do własnych potrzeb (w szczególności jego wygląd). Życzę miłego użytkowania i zapraszam o opiniowanie na moim blogu: http://www.wlasocha.pl/portfolio/audio-web-player.
