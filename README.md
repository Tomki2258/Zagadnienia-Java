### Podstawy Javy i zarządzanie pamięcią

#### 1. Alokacja pamięci na stosie, a alokacja na stercie w Javie
W Javie pamięć dzielona jest na stos (stack) i stertę (heap). Zmiennie lokalne i wywołania metod są przechowywane na stosie. Stos jest szybki, ale ma ograniczoną pojemność i działa na zasadzie LIFO (Last In, First Out). Sterta jest używana do przechowywania obiektów, które mają dłuższy czas życia i mogą być dostępne globalnie. Jest większa niż stos, ale wolniejsza z powodu konieczności zarządzania pamięcią dynamiczną i przeprowadzania operacji garbage collection .

#### 2. Różnica między inicjalizacją `String s = "abc"` oraz `String s = new String("abc")`
Przy inicjalizacji `String s = "abc"` używany jest String Pool, co oznacza, że jeżeli identyczny ciąg znaków już istnieje w puli, to zwrócony zostanie referencja do istniejącego obiektu. `String s = new String("abc")` tworzy nowy obiekt na stercie, nawet jeśli taki sam ciąg znaków istnieje już w String Pool. Pierwszy sposób jest bardziej efektywny pod względem pamięci .

#### 3. Napisz wrapper dla dowolnego typu prostego
Wrapper dla typu prostego (np. int) w Javie wygląda następująco:
```java
public class IntWrapper {
    private int value;

    public IntWrapper(int value) {
        this.value = value;
    }

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }
}
```

#### 4. Czym jest klonowanie i kopiowanie obiektu?
Klonowanie w Javie oznacza tworzenie kopii obiektu. Implementacja interfejsu `Cloneable` oraz nadpisanie metody `clone()` umożliwia płytkie klonowanie, gdzie kopiowane są tylko referencje obiektów. Głębokie klonowanie oznacza kopiowanie wszystkich obiektów złożonych na nowo. Alternatywnie, kopiowanie można zrealizować poprzez konstruktor kopiujący, który tworzy nową instancję obiektu kopiując wartości z innego obiektu  .

#### 5. Składnia i działanie konstruktora
Konstruktor to specjalna metoda wywoływana podczas tworzenia obiektu. Może przyjmować argumenty i inicjalizować pola klasy. Przykład wywołania konstruktora klasy tej samej klasy i klasy nadrzędnej:
```java
public class Parent {
    public Parent() {
        System.out.println("Parent constructor");
    }
}

public class Child extends Parent {
    public Child() {
        super(); // wywołanie konstruktora klasy nadrzędnej
        System.out.println("Child constructor");
    }

    public Child(int x) {
        this(); // wywołanie konstruktora tej samej klasy
        System.out.println("Child constructor with parameter");
    }
}
```
    

#### 6. Do czego służą funkcje `System.gc()` i `Runtime.gc()`?
Funkcje `System.gc()` i `Runtime.gc()` sugerują maszynie wirtualnej Java uruchomienie garbage collectora. Nie gwarantują jednak jego natychmiastowego uruchomienia. Obie metody działają w ten sam sposób, ale `Runtime.gc()` jest wywoływana na instancji klasy `Runtime` .

#### 7. Wymień i omów wszystkie sposoby użycia słowa kluczowego `final`
Słowo kluczowe `final` może być używane na trzy sposoby:
1. **Zmienne**: Zmienne oznaczone jako `final` nie mogą zmieniać wartości po inicjalizacji.
2. **Metody**: Metody oznaczone jako `final` nie mogą być nadpisywane przez klasy dziedziczące.
3. **Klasy**: Klasy oznaczone jako `final` nie mogą być dziedziczone przez inne klasy.
Stosowanie `final` pomaga zapewnić niezmienność i bezpieczeństwo kodu poprzez zapobieganie modyfikacjom .

### Programowanie obiektowe

#### 8. Omów porównawczo dziedziczenie klas i implementację interfejsów
Dziedziczenie klas (extends) pozwala na użycie metod i pól z klasy nadrzędnej oraz na nadpisywanie ich. Można dziedziczyć tylko jedną klasę. Implementacja interfejsów (implements) umożliwia używanie wielu interfejsów, które deklarują metody bez ich implementacji. Klasa implementująca interfejs musi zaimplementować wszystkie jego metody .

#### 9. Omów porównawczo klasy abstrakcyjne i interfejsy
Klasy abstrakcyjne mogą zawierać zarówno deklaracje jak i definicje metod oraz pola. Mogą być dziedziczone tylko przez jedną klasę. Interfejsy zawierają tylko deklaracje metod (do Javy 8) i są implementowane przez dowolną liczbę klas. Od Javy 8, interfejsy mogą mieć domyślne i statyczne metody, a od Javy 9, metody prywatne .

#### 10. Omów polimorfizm
Polimorfizm pozwala na korzystanie z obiektów różnych klas przez ten sam interfejs. Umożliwia to traktowanie obiektów różnego typu w sposób jednolity. Polimorfizm może być uzyskany przez dziedziczenie oraz przez implementację interfejsów. Przykładem jest nadpisywanie metod, gdzie metoda w klasie podrzędnej ma taką samą sygnaturę jak w klasie nadrzędnej .

#### 11. Omów enkapsulację. Przedstaw modyfikatory dostępu w kontekście enkapsulacji
Enkapsulacja to ukrywanie szczegółów implementacji obiektu i udostępnianie tylko niezbędnego interfejsu. Modyfikatory dostępu:
- **private**: dostęp tylko w obrębie tej samej klasy.
- **default (package-private)**: dostęp w obrębie tego samego pakietu.
- **protected**: dostęp w obrębie tego samego pakietu oraz w klasach dziedziczących.
- **public**: dostępny z każdego miejsca.
Enkapsulacja pomaga chronić dane i zapobiegać ich niewłaściwemu użyciu .

#### 12. Przedstaw rodzaje asocjacji między klasami
Rodzaje asocjacji:
- **Asocjacja**: ogólna relacja, w której obiekty mogą odwoływać się do siebie nawzajem.
- **Agregacja**: specjalny typ asocjacji, który reprezentuje relację całość-część, gdzie część może istnieć niezależnie od całości.
- **Kompozycja**: silniejsza forma agregacji, w której części nie mogą istnieć bez całości i ich cykle życia są współzależne .

### Kolekcje

#### 13. Omów interfejs `Collection`
Interfejs `Collection` jest podstawowym interfejsem w hierarchii kolekcji w Javie. Definiuje metody dla operacji na grupie obiektów, takie jak dodawanie, usuwanie, przeszukiwanie i iteracja. `Collection` jest superinterfejsem dla bardziej specjalistycznych interfejsów jak `List`, `Set`, i `Queue` .

#### 14. Porównaj klasy `LinkedList` i `ArrayList`
`LinkedList` to implementacja listy połączonej, która oferuje efektywne operacje dodawania i usuwania elementów, szczególnie na początku i końcu listy. `ArrayList` to dynamiczna tablica, która oferuje szybki dostęp do elementów dzięki indeksom, ale operacje dodawania i usuwania są wolniejsze, ponieważ mogą wymagać przesunięcia elementów. `LinkedList` jest bardziej pamięciożerna, a `ArrayList` jest lepsza do przypadkowego dostępu .

#### 15. W C++ jest typ `std::multimap`. Jak zrekonstruować jego działanie w Javie?
`std::multimap` w C++ przechowuje klucze z wieloma wartościami. W Javie można to osiągnąć używając `Map<K, List<V>>`. Przykład:
```java
Map<String, List<Integer>> multimap = new HashMap<>();
multimap.put("key1", new ArrayList<>(Arrays.asList(1, 2, 3)));
multimap.put("key2", new ArrayList<>(

Arrays.asList(4, 5, 6)));
```

### Wyjątki

#### 16. Omów składnię i zastosowanie wyjątków
Wyjątki w Javie to mechanizm obsługi błędów. Składnia `try-catch` umożliwia przechwytywanie i obsługę wyjątków. `finally` może być używany do wykonania kodu niezależnie od tego, czy wyjątek został zgłoszony, czy nie. `throw` służy do zgłaszania wyjątków, a `throws` deklaruje, jakie wyjątki metoda może zgłosić.

#### 17. Wyjątek `Exception` a `RuntimeException`, podaj wyjaśnij różnicę i podaj przykład
`Exception` to ogólna klasa dla wyjątków kontrolowanych, które muszą być deklarowane lub obsługiwane. `RuntimeException` to podklasa `Exception`, reprezentująca wyjątki niekontrolowane, które są błędami programistycznymi i nie muszą być deklarowane ani obsługiwane. Przykład:
```java
public void method() throws IOException { // Exception
    throw new IOException();
}

public void method() { // RuntimeException
    throw new NullPointerException();
}
```

### Strumienie:

#### 18. Opisz trzy metody pośrednie w strumieniu
Trzy przykłady metod pośrednich:
1. `filter(Predicate<T>)`: filtruje elementy strumienia, pozostawiając te, które spełniają podane kryterium.
2. `map(Function<T, R>)`: przekształca elementy strumienia, stosując podaną funkcję.
3. `sorted()`: sortuje elementy strumienia w naturalnym porządku lub zgodnie z podanym komparatorem.

#### 19. Omów kolektory
Kolektory w Javie, dostępne w klasie `Collectors`, umożliwiają zbieranie elementów strumienia do kolekcji lub agregowanie ich wyników. Przykłady to `toList()`, `toSet()`, `joining()`, `groupingBy()`, `partitioningBy()`. Są one używane w metodzie `collect()` strumienia.

### Testowanie

#### 20. Przedstaw motywację do stosowania testów, omów Test Driven Development
Testowanie kodu zapewnia jego poprawność, wydajność i bezpieczeństwo. Test Driven Development (TDD) to podejście, w którym najpierw piszemy testy jednostkowe, a następnie kod, który te testy przechodzi. Pomaga to w utrzymaniu czystego, dobrze zaprojektowanego kodu oraz zmniejsza liczbę błędów.

#### 21. Parametryzacja testów
Parametryzacja testów pozwala na uruchamianie tego samego testu z różnymi danymi wejściowymi. W JUnit 5 można to osiągnąć za pomocą adnotacji `@ParameterizedTest` i dostarczenia zestawów danych poprzez metody, pliki CSV lub źródła zewnętrzne.

### Pakiety

#### 22. Zasady tworzenia i zastosowanie pakietów
Pakiety grupują powiązane klasy i interfejsy, co ułatwia zarządzanie nimi oraz kontrolę dostępu. Tworzenie pakietu wymaga użycia deklaracji `package` na początku pliku Java. Użycie pakietów pozwala na uniknięcie konfliktów nazw oraz poprawia organizację kodu.

#### 23. Czym są pliki JAR? Omów ich tworzenie i wykorzystanie. Omów manifest
Pliki JAR (Java ARchive) to archiwa zawierające skompilowane pliki klas, metadane i zasoby. Są używane do dystrybucji aplikacji Java. Tworzenie plików JAR odbywa się za pomocą narzędzia `jar`, a manifest (`META-INF/MANIFEST.MF`) zawiera informacje o zawartości archiwum, w tym opcjonalne atrybuty, jak `Main-Class`, definiujące punkt wejścia aplikacji.

#### 24. Wymień i omów trzy zastosowania Mavena
Maven to narzędzie do zarządzania projektami Java. Jego trzy główne zastosowania to:
1. **Zarządzanie zależnościami**: Automatyczne pobieranie i zarządzanie bibliotekami z repozytoriów.
2. **Budowanie projektu**: Kompilacja, testowanie i pakowanie aplikacji.
3. **Konfiguracja projektu**: Centralizacja konfiguracji w pliku `pom.xml`, co ułatwia utrzymanie i automatyzację procesu budowy.

#### 25. Elementy składowe pliku `pom.xml`
Plik `pom.xml` zawiera:
- **project**: Element główny.
- **modelVersion**: Wersja modelu POM.
- **groupId**: Identyfikator grupy.
- **artifactId**: Identyfikator artefaktu.
- **version**: Wersja projektu.
- **dependencies**: Lista zależności projektu.
- **build**: Informacje o budowaniu projektu, w tym wtyczki.

### Programowanie generyczne

#### 26. Typy generyczne a typ `Object`
Typy generyczne zapewniają bezpieczeństwo typów bez konieczności rzutowania. Pozwalają na tworzenie klas, interfejsów i metod, które operują na typach określonych w czasie kompilacji. Typ `Object` wymaga rzutowania i nie daje takiej samej elastyczności i bezpieczeństwa typów .

#### 27. Ograniczenia typów generycznych
Typy generyczne mogą być ograniczane za pomocą słów kluczowych `extends` (dla górnych ograniczeń) oraz `super` (dla dolnych ograniczeń). Przykłady:
```java
public <T extends Number> void example(T t) { }
public <T super Integer> void example(T t) { }
```

#### 28. Interfejsy funkcyjne: `Supplier`, `Predicate`, `Consumer`, `Function`
- **Supplier**: dostarcza obiekty określonego typu.
- **Predicate**: sprawdza warunek na obiekcie, zwraca `boolean`.
- **Consumer**: wykonuje operację na obiekcie, nie zwraca wyniku.
- **Function**: przekształca obiekt typu T na obiekt typu R.

#### 29. Omów szablon `Optional`
`Optional` jest kontenerem dla wartości, który może być pusty lub zawierać wartość. Pomaga uniknąć `NullPointerException`. Przykład:
```java
Optional<String> optional = Optional.of("value");
optional.ifPresent(System.out::println);
String orElse = optional.orElse("default");
```

### Wątki

#### 30. Omów synchronizację wątków
Synchronizacja wątków w Javie zapobiega jednoczesnemu dostępowi do zasobów współdzielonych przez wiele wątków, co może prowadzić do niepożądanych rezultatów. Słowo kluczowe `synchronized` zapewnia blokadę na metodach lub blokach kodu. Można także używać obiektów `Lock` z pakietu `java.util.concurrent.locks` .

#### 31. Omów cykl życia wątku
Cykl życia wątku obejmuje stany:
- **New**: Wątek został utworzony, ale nie rozpoczął działania.
- **Runnable**: Wątek jest gotowy do działania i czeka na przydział procesora.
- **Blocked**: Wątek czeka na zwolnienie blokady.
- **Waiting**: Wątek czeka na sygnał od innego wątku.
- **Timed Waiting**: Wątek czeka na określony czas.
- **Terminated**: Wątek zakończył wykonanie.

### JavaFX

#### 32. Czym są wydarzenia i jak je obsługiwać?
Wydarzenia (events) w JavaFX to akcje, takie jak kliknięcia myszy czy naciśnięcia klawiszy. Obsługuje się je poprzez dodanie odpowiednich nasłuchiwaczy (event handlers) do elementów interfejsu. Przykład obsługi kliknięcia przycisku:
```java
Button button = new Button("Click me");
button.setOnAction(event -> System.out.println("Button clicked"));
```

#### 33. Omów zależność między typami `Scene` i `Stage`
`Stage` reprezentuje główne okno aplikacji JavaFX, a `Scene` zawiera hierarchię węzłów (elementów interfejsu) wyświetlanych w tym oknie. Jeden `Stage` może mieć wiele `Scene`, ale w danym momencie tylko jedna `Scene` może być aktywna. Przykład:
```java
Stage stage = new Stage();
Scene scene = new Scene(new Group(new Button("Click me")));
stage.setScene(scene);
stage.show();
```
