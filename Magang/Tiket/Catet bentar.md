```
package com.tiket.web.dashboard.page.ttd.Ignis.SalesReportPage;  
  
import com.tiket.model.Session;  
import org.openqa.selenium.WebDriver;  
  
public class IgnisSalesReportPageDweb<T extends WebDriver> extends IgnisSalesReportPageWeb<T> {  
    public IgnisSalesReportPageDweb(Session<T> session) {  
        super(session);  
    }  
}
```

```
package com.tiket.web.dashboard.page.ttd.Ignis.SalesReportPage;  
  
import com.tiket.model.Session;  
import org.openqa.selenium.WebDriver;  
  
public class IgnisSalesReportPageMweb<T extends WebDriver> extends IgnisSalesReportPageWeb<T> {  
    public IgnisSalesReportPageMweb(Session<T> session) {  
        super(session);  
    }  
}
```

```
package com.tiket.web.dashboard.page.ttd.Ignis.SalesReportPage;  
  
import com.tiket.core.CoreFunctions;  
import com.tiket.model.Locator;  
import com.tiket.model.Session;  
import com.tiket.testbase.Configs;  
import com.tiket.web.WebPage;  
import com.tiket.web.dashboard.page.ttd.Ignis.OrderReportPage.IgnisOrderReportPageDweb;  
import com.tiket.web.dashboard.page.ttd.Ignis.OrderReportPage.IgnisOrderReportPageMweb;  
import com.tiket.web.dashboard.page.ttd.Ignis.OrderReportPage.IgnisOrderReportPageWeb;  
import org.apache.commons.lang3.NotImplementedException;  
import org.openqa.selenium.By;  
import org.openqa.selenium.WebDriver;  
import org.openqa.selenium.WebElement;  
  
import java.util.List;  
import java.util.NoSuchElementException;  
  
public class IgnisSalesReportPageWeb<T extends WebDriver> extends WebPage<T> {  
    public IgnisSalesReportPageWeb(Session<T> session) {  
        super(session);  
    }  
  
    public static <T extends WebDriver> IgnisSalesReportPageWeb<?> getInstance(Session<T> session) {  
        switch (Configs.PLATFORM) {  
            case DWEB -> {  
                return new IgnisSalesReportPageDweb<>(session);  
            }  
            case AMWEB, IMWEB, ANDROID, IOS -> {  
                return new IgnisSalesReportPageMweb<>(session);  
            }  
            default -> throw new NotImplementedException("Unsupported platform: " + Configs.PLATFORM);  
        }  
    }  
  
    // Home  
    private static final Locator MENU_REPORT_DROPDOWN = new Locator("MENU_REPORT_DROPDOWN", By.xpath("//div[@class='menu__item--nested' and .//span[@class='menu__title' and text()='Report']]"));  
    private static final Locator SALES_REPORT_ANCHOR = new Locator("SALES_REPORT_ANCHOR", By.xpath("//a[@href='/ignis/sales-report']"));  
  
    // Sales report page  
    private static final Locator THINGSTODO_DROPDOWN = new Locator("THINGSTODO_DROPDOWN", By.xpath("//div[@class='filter__product']//fieldset"));  
    private static final Locator THINGSTODO_DROPDOWN_SELECTION = new Locator("THINGSTODO_DROPDOWN_SELECTION", By.xpath("//div[@class='filter__product_popup']"));  
    private static final Locator PACKAGE_DROPDOWN = new Locator("PACKAGE_DROPDOWN", By.xpath("//div[@class='filter__packages']//fieldset"));  
    private static final Locator PACKAGE_DROPDOWN_SELECTION = new Locator("PACKAGE_DROPDOWN_SELECTION", By.xpath("//div[@class='list__item' and .//div[@class='item__text']]"));  
    private static final Locator TIME_PERIOD_DROPDOWN = new Locator("TIME_PERIOD_DROPDOWN", By.xpath("//div[@class='filter__date-range']"));  
    private static final Locator TIME_PERIOD_POPUP = new Locator("TIME_PERIOD_POPUP", By.xpath("//div[@class='date-range__popup']"));  
    private static final Locator TIME_PERIOD_POPUP_DROPDOWN = new Locator("TIME_PERIOD_POPUP_DROPDOWN", By.xpath("//div[@class='date-range__popup']//fieldset"));  
    private static final Locator TIME_PERIOD_POPUP_DROPDOWN_SELECTION = new Locator("TIME_PERIOD_POPUP_DROPDOWN_SELECTION",  By.xpath("//input[@class='menu-item']"));  
    private static final Locator TIME_PERIOD_SAVE_BUTTON = new Locator("TIME_PERIOD_SAVE_BUTTON", By.xpath("//button[@class='btn btn-primary actions-item__search']"));  
    private static final Locator BY_VISIT_DATE_RADIOBUTTON = new Locator("BY_VISIT_DATE_RADIOBUTTON", By.xpath("//input[@value='VISIT_DATE']"));  
    private static final Locator BY_TRANSACTION_DATE_RADIOBUTTON = new Locator("BY_TRANSACTION_DATE_RADIOBUTTON", By.xpath("//input[@value='TRANSACTION_DATE']"));  
    private static final Locator SEARCH_BUTTON = new Locator("SEARCH_BUTTON", By.xpath("//button[@class='btn btn-tertiary filter-actions-item__search']"));  
  
    public void goToSalesReportPage() {  
        driverTools.click(MENU_REPORT_DROPDOWN);  
  
        driverTools.waitForElementToAppear(SALES_REPORT_ANCHOR);  
        driverTools.click(SALES_REPORT_ANCHOR);  
    }  
  
    public String selectProduct(String productName) {  
        return selectProduct(productName, THINGSTODO_DROPDOWN, THINGSTODO_DROPDOWN_SELECTION);  
    }  
  
    public String selectPackage(String packageName) {  
        return selectPackage(packageName, PACKAGE_DROPDOWN, PACKAGE_DROPDOWN_SELECTION);  
    }  
  
    public String selectProduct(String productName, Locator dropdown, Locator dropdownSelection) {  
        driverTools.waitForElementToAppear(dropdown);  
        driverTools.waitForElementToBeClickable(dropdown);  
        driverTools.click(dropdown);  
  
        driverTools.dummyWait(1);  
        List<WebElement> productNames = driverTools.elementsUntilExist(dropdownSelection).get();  
  
        String chosenProductText = "";  
        if (productName.equalsIgnoreCase("random")) {  
            int randomInt = CoreFunctions.generateRandomInt(1, productNames.size()-1);  
            chosenProductText = driverTools.getText(productNames.get(randomInt));  
            driverTools.click(productNames.get(randomInt));  
        } else {  
            for (WebElement e : productNames) {  
                String productNameText = driverTools.getText(e);  
                if (productNameText.equalsIgnoreCase(productName)) {  
                    chosenProductText = productNameText;  
                    driverTools.click(e);  
                    break;  
                }  
            }  
  
            if (chosenProductText.isEmpty()) {  
                throw new NoSuchElementException("There is no option for '" + productName + "' on Product selection");  
            }  
        }  
        return chosenProductText;  
    }  
  
    public String selectPackage(String packageName, Locator dropdown, Locator dropdownSelection) {  
        driverTools.waitForElementToAppear(dropdown);  
        driverTools.click(dropdown);  
  
        driverTools.dummyWait(1);  
        List<WebElement> productNames = driverTools.elementsUntilExist(dropdownSelection).get();  
  
        String chosenPackageText = "";  
        if (packageName.equalsIgnoreCase("random")) {  
            int randomInt = CoreFunctions.generateRandomInt(1, productNames.size()-1);  
            chosenPackageText = driverTools.getText(productNames.get(randomInt));  
            driverTools.click(productNames.get(randomInt));  
        } else {  
            for (WebElement e : productNames) {  
                String productNameText = driverTools.getText(e);  
                if (productNameText.equalsIgnoreCase(packageName)) {  
                    chosenPackageText = productNameText;  
                    driverTools.click(e);  
                    break;  
                }  
            }  
  
            if (chosenPackageText.isEmpty()) {  
                throw new NoSuchElementException("There is no option for '" + packageName + "' on Package selection");  
            }  
        }  
        return chosenPackageText;  
    }  
  
    // The custom selection hasn't been implemented  
    public String selectTimePeriod(String timePeriod) {  
        driverTools.waitForElementToAppear(TIME_PERIOD_DROPDOWN);  
        driverTools.click(TIME_PERIOD_DROPDOWN);  
  
        driverTools.waitForElementToAppear(TIME_PERIOD_POPUP);  
  
        driverTools.waitForElementToAppear(TIME_PERIOD_POPUP_DROPDOWN);  
        driverTools.click(TIME_PERIOD_POPUP_DROPDOWN);  
  
        driverTools.dummyWait(1);  
        List<WebElement> timePeriods = driverTools.elementsUntilExist(TIME_PERIOD_POPUP_DROPDOWN_SELECTION).get();  
  
        String chosenTimePeriodText = "";  
        for (WebElement e : timePeriods) {  
            String timePeriodText = driverTools.getText(e);  
            if (timePeriodText.equalsIgnoreCase(timePeriod)) {  
                chosenTimePeriodText = timePeriodText;  
                driverTools.click(e);  
                break;  
            }  
        }  
  
        if (chosenTimePeriodText.isEmpty()) {  
            throw new NoSuchElementException("There is no option for '" + timePeriod + "' on Package selection");  
        }  
  
        driverTools.click(TIME_PERIOD_SAVE_BUTTON);  
  
        return chosenTimePeriodText;  
    }  
  
    public void setVisitOrTransactionFilter(String filter) {  
        switch (filter.toLowerCase()) {  
            case "visit" -> {  
                driverTools.click(BY_VISIT_DATE_RADIOBUTTON);  
            }  
            case "transaction" -> {  
                driverTools.click(BY_TRANSACTION_DATE_RADIOBUTTON);  
            }  
            default -> {  
                throw new NoSuchElementException("There is no filter '"+ filter +"'");  
            }  
        }  
    }  
  
    public void clickSearch() {  
        driverTools.click(SEARCH_BUTTON);  
    }  
}
```


```
package com.tiket.web.dashboard.test.ttd.sales_report;  
  
import com.tiket.annotation.Author;  
import com.tiket.annotation.Module;  
import com.tiket.annotation.Tribe;  
import com.tiket.annotation.Vertical;  
import com.tiket.model.Session;  
import com.tiket.testbase.BaseTest;  
import com.tiket.web.WebTest;  
import com.tiket.web.dashboard.page.ttd.Ignis.LoginPage.IgnisLoginPageWeb;  
import com.tiket.web.dashboard.page.ttd.Ignis.PartnerPage.IgnisPartnerPageWeb;  
import com.tiket.web.dashboard.page.ttd.Ignis.SalesReportPage.IgnisSalesReportPageWeb;  
import com.tiket.web.dashboard.page.ttd.Ignis.SelectPartnerPage.IgnisSelectPartnerPageWeb;  
import org.testng.annotations.Test;  
  
import java.util.Map;  
  
import static com.tiket.testdata.TestData.getParam;  
  
public class TtdSalesReportTest extends WebTest {  
  
    @Author(names = {"Rizki"})  
    @Module(name = "SalesReport")  
    @Tribe(name = "Ignis")  
    @Vertical(name = "TTD")  
    @Test  
    public void testIgnisFilterSalesReportByTransactionDate() {  
        Map<String, String> param = getParam("testIgnisFilterSalesReportByTransactionDate");  
        BaseTest.paramsThreadLocal.set(param);  
  
        String username = param.get("username");  
        String password = param.get("password");  
  
        String partnerName = param.get("partnerName");  
        String productName = param.get("productName");  
        String packageName = param.get("packageName");  
        String timePeriod = param.get("timePeriod");  
        String filter = param.get("filter");  
  
        Session<?> session = BaseTest.sessionThreadLocal.get();  
        IgnisLoginPageWeb<?> ignisLoginPageWeb = IgnisLoginPageWeb.getInstance(session);  
        IgnisSelectPartnerPageWeb<?> ignisSelectPartnerPageWeb = IgnisSelectPartnerPageWeb.getInstance(session);  
        IgnisSalesReportPageWeb<?> ignisSalesReportPageWeb = IgnisSalesReportPageWeb.getInstance(session);  
  
        step("Login to Ignis");  
        ignisLoginPageWeb.loginAsSpecificUser(username, password);  
  
        step("Select any partners");  
        ignisSelectPartnerPageWeb.selectPartner(partnerName);  
  
        step("Go to Sales Report page");  
        ignisSalesReportPageWeb.goToSalesReportPage();  
  
        step("Select any product and its packages");  
        ignisSalesReportPageWeb.selectProduct(productName);  
        ignisSalesReportPageWeb.selectPackage(packageName);  
  
        step("Set the Time Period as Last 7 Days, click Save");  
        ignisSalesReportPageWeb.selectTimePeriod(timePeriod);  
  
        step("Set the filter as By Transaction Date");  
        ignisSalesReportPageWeb.setVisitOrTransactionFilter(filter);  
  
        step("Click Search");  
        ignisSalesReportPageWeb.clickSearch();  
    }  
  
}
```


mvn test -Dthreads=4 -Dsessions=4 -Dplatform=dWeb -Dtestdata=local -Dtribe=Ignis -Dmodule=SalesReport -Dtestname=all -Dtesttype=all -Denv=gk