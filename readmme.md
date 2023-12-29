In-depth session: Cypress 
https://www.saucedemo.com/
standard_user / secret_sauce <- dane do logowania. Inne konta spowodują inny widok użytkownika!!!

UWAGA!!! wszystkie testy odpalamy w terminalu. W przypadku korzystania z Cypress UI - przed każdym ponownym uruchomieniem - trzeba zamknąć i otworzyć na nowo Cypressa. (Wynika to z architektury strony która trzyma w pamięci zalogowaną sesję przez jakiś czas. Z tego powodu - testy mogą fajlować) 
Przygotowanie projektu:
Utworzyć folder dla projektu
Stworzyć repo na GitHubie
Sklonować repo 
Zmień folder na sklonowany
Stworzyć README.md, skopiować treść tego pliku
Konfiguracja projektu:
Zainstaluj Cypress
Skonfiguruj projekt dla e2e testów (poprzez Cypress UI)
Skonfiguruj “baseUrl” w cypress.config.js 
Stwórz cypress.env.json plik oraz uzupełnij go: 
{
    "username": "standard_user",
    "password": "secret_sauce",
    "firstName": "testUser",
    "lastName": "testUserl",
    "postalCode": "52-131"
  }
W folderze “Cypress” stwórz folder “pages”
Upewnij się iż drzewo projektu wygląda następująco:

Zadania:
W folderze “pages” stwórz plik o nazwie “loginPage.js”
stwórz klasę która reprezentuje stronę logowania
stwórz selektory dla pól username / password oraz przycisku <Login>
stwórz następne metody:
visit() -> powinna prowadzić na stronę logowania 
fillUsername(username) -> powinna uzupełniać pole username z wykorzystaniem zmiennych środowiskowych
fillPassword(password) -> powinna uzupełniać pole password z wykorzystaniem zmiennych środowiskowych
submit() -> powinna naciskać przycisk <Login>
stwórz obiekt LoginPage();

W pliku “commands.js” w folderze “support”:
Importuj: “import LoginPage from '../pages/loginPage';”
Stwórz własną komendę “login” która powinna uzupełnić wszystkie pola logowania oraz kliknąć przycisk <Login>

W folderze “e2e” stwórz plik “login.spec.cy.js”:
Importuj “import '../support/commands.js';”
Napisz test, który przetestuje poprawne logowanie. W postaci asercji użyj url strony która otwiera się po zalogowaniu:
wykorzystaj komendę z poprzedniego kroku
url ma uwzględniać “baseUrl”
Odpal test poprzez terminal

W folderze “pages” stwórz plik “inventoryPage.js”:
stwórz klasę która reprezentuje stronę z towarami
stwórz selektory dla przycisku <Add to cart> oraz “koszyku”
stwórz metody:
addToCart(itemName) -> wyszukuje i klika na element zawierający nazwę produktu; na stronie produktu klika przycisk <Add to cart>
getShoppingCartBadgeCount() -> sprawdza licznik koszyku po dodaniu produktu
goToShoppingCart() -> kilka na koszyk
stwórz obiekt “InventoryPage”
W folderze “e2e” stwóz plik “addItem.spec.cy.js”:
Importuj: import InventoryPage from '../pages/inventoryPage'; import '../support/commands.js';
Napisz test który sprawdzi dodanie przedmiotu do koszyku:
dodaj sekcję “beforeEach” z stworzoną komendą “login()”
w postaci pierwszej asercji użyj licznik dodanych przedmiotów w koszyku
przejdź bezpośrednio do koszyku
w postaci drugiej asercji użyj url ze strony koszyka
W folderze “pages” stwórz plik “cartPages”
stwórz klasę reprezentującą stronę koszyka
stwórz selektor dla przycisku <Checkout>
stwórz metodę “proceedToCheckout()”
stwórz obiekt “CartPage”
W pliku “commands.js” stwórz nową komendę “addProduct” która będzie dodawala wybrany produkt do koszyku 
W folderze “e2e” stwórz plik “cart.spec.cy.js”
Importuj: import CartPage from '../pages/cartPage';
import '../support/commands.js';
Napisz test który sprawdzi przycisk <Checkout>:
dodaj w sekcji “beforeEach” komendy “login” oraz “addProduct(‘produkt’)
kliknij na przycisk <Checkout>
w postaci asercji uzyj url z strony “/checkout-step-one.html” (uwzględniając baseUrl)
W folderze “pages” stwórz plik “checkoutStepOnePage.js”
stwórz klasę “CheckoutStepOnePage”
stwórz selektory reprezentujące pola “firstname”, “lastname”, “postalcode” oraz przycisk <Continue>
stwórz metody(dane powinne byc zaciągane ze zmiennych środowiskowych):
fillFirstName(firstname)
fillLastName(lastname)
fillPostalCode(postalCode)
continue()
stwórz obiek CheckoutStepOnePage
W folderze “pages” stwórz plik “checkoutStepTwoPage.js”
stwórz klasę “CheckoutStepTwoPage”
stwórz selektor dla przycisku <Finish>
stwórz metodę która klika w przycisk <Finish>
stwórz obiekt “CheckoutStepTwoPage”
W pliku “commands.js” stwórz komendę “proceedToCheckout()”
W folderze “e2e” stwórz plik “checkout.spec.cy.js”
Importuj: import CheckoutStepOnePage from '../pages/checkoutStepOnePage.js'; import CheckoutStepTwoPage from '../pages/checkoutStepTwoPage.js';import '../support/commands.js';
	stwórz	test który sprawdzi funkcjonalność “checkout”
w beforeEach wykorzystaj wszystkie stworzone komendy
test powinien wypełnić wszystkie niezbędne pola na stronie “CheckoutStepOne” oraz kliknąć <Continue>
w postaci pierwszej asercji wykorzystaj url z następnej strony (z uwzględnieniem baseUrl)
w następnym kroku test powinien kliknąć przycisk <Finish>
w postaci asercji wykorzystaj url z następnej strony

Zakończenie:
Odpal wszystkie testy
Dodaj komentarzy w kodzie
Sprawdź stylistykę kodu
Git add / commit / push


