Notes:
ELEMENT : The element that will be interacted.

---
## Element Declaration
### Button
For button, we need to explicitly pick the button element.
```java
private static final Locator APPLY_FILTER_BUTTON = new Locator("APPLY_FILTER_BUTTON", By.xpath("//button[contains(@class,'button variant-secondary')]"));
```
### Dropdown
For the dropdown, we select the most outside container. We could use div element for this.
```java
private static final Locator SUBSIDY_DROPDOWN = new Locator("SUBSIDY_DROPDOWN", By.xpath("//div[@class='filters-item subsidy-filter']"));
```
### Dropdown Selection
This the container that shown after the dropdown is pressed.
```java
private static final Locator SUBSIDY_DROPDOWN_SELECTION = new Locator("SUBSIDY_DROPDOWN_SELECTION", By.xpath("//div[@class='menu-item']"));
```
### Text


---
## Functions
### get
Moving to a different pages. We put the link as the parameters. 
```java
driver.get("https://gatotkaca.tiket.com/ignis/reports"
```
### click
This is used for clicking button.
```java
driverTools.click(APPLY_FILTER_BUTTON);
```
### waitForElementToAppear
Some element will only shown after a certain event is triggered like clicking a dropdown and stuff.
```java
driverTools.waitForElementToAppear(LOADING_CONTAINER);
```
### waitForElementToDisappear
Waiting for the element to disappear first before executing the next action;
```java
driverTools.waitForElementToDisappear(LOADING_CONTAINER);
```
### getText
Getting the text of a certain elements.
### waitForWebToLoad
Waiting for the web to stop loading. This is usually executed when we want to open another page (changing the url).
```java
driverTools.waitForWebToLoad();
```
### elementsUntilExist
Return the elements when the elements exists. This uses cases is similar to `waitForElementToAppear`. 
```java
List<WebElement> productNames = driverTools.elementsUntilExist(dropdownSelection).get();
```
