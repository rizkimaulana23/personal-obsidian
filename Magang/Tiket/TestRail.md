## Introduction
## Structure
![[Screenshot 2025-07-21 at 14.24.30.png]]

The one that we do as SDET is only the P0 API, that is the highest priority of API Automation. If we open the P0 API folder, it will show us all of the test case categories.

![[Screenshot 2025-07-21 at 14.26.55.png]]

If we open the categories, then we could actually see the test cases.

![[Screenshot 2025-07-21 at 14.27.59.png]]

Inside of the test case, there are details about what the type, pic, reviewed by, and other things.

![[Screenshot 2025-07-21 at 14.29.23.png]]

There are also the main important part that is the Steps and The Expected Results.

![[Screenshot 2025-07-21 at 14.30.28.png]]
![[Screenshot 2025-07-21 at 14.30.42.png]]
## Coding Structure
### Making the Class
First, we make a class based on the categories of the test case it self (the folder that holds all of the test case).

```java
public class TTDAdminsProductsProductListGET extends AbstractApiV2 {
}
```

The class, I mean every class will extend the class `AbstractApiV2`. The functionality of this class is still unknown. Let's study it later.
### Making the Constructor
For the constructor, this is usually the case for every Class. The map will receive the data of the test case itself. The data of this is included in the Google Sheets test data.

```java
public TTDAdminsProductsProductListGET(Properties map) {  
  super(null, null, map);  
  UriHelper uriHelper = new UriHelper(P.API.get("baseUrlGK"),  
      P.API.get("baseUrlProd"),  
      P.API.get("baseUrlPreProd"));  
  replaceUrlPlaceholder("baseUrl", uriHelper.getUri());  
}
```

Then the later code will be able to get that data by accessing the Class's `properties` properties. For example:

```java
this.setHeader("currency", Common.stringValueOf(this.getProperties().get("currency"))
```
### Categorizing The Test Case
We categorize each of the test case by the TestType as enums. 

In this example we will discuss and thoroughly examine the example this test case category:

This is the code:
```java
private enum TestType {  
  valid_positive_test_cases, valid_page_size, valid_statuses_inactive, valid_statuses_hidden, valid_existing_partners,  
  valid_primary_category, invalid_primary_category, invalid_statuses, invalid_non_existing_partners, valid_sort_field_sort_direction,  
  valid_title_contains;  
  
  public static TestType parse(String testType) {  
    switch (testType){  
      case "valid_positive_test_cases" -> {  
        return valid_positive_test_cases;  
      }  
      case "valid_page_size" -> {  
        return valid_page_size;  
      }  
      case "valid_statuses_inactive" -> {  
        return valid_statuses_inactive;  
      }  
      case "valid_statuses_hidden" -> {  
        return valid_statuses_hidden;  
      }  
      case "valid_existing_partners" -> {  
        return valid_existing_partners;  
      }  
      case "valid_primary_category" -> {  
        return valid_primary_category;  
      }  
      case "invalid_primary_category" -> {  
        return invalid_primary_category;  
      }  
      case "invalid_statuses" -> {  
        return invalid_statuses;  
      }  
      case "invalid_non_existing_partners" -> {  
        return invalid_non_existing_partners;  
      }  
      case "valid_sort_field_sort_direction" -> {  
        return valid_sort_field_sort_direction;  
      }  
      case "valid_title_contains" -> {  
        return valid_title_contains;  
      }  
      default -> throw new NotImplementedException(String.format("Test type not exist", testType));  
    }  
  }  
}
```

This is the test cases in TestRail:

![[Screenshot 2025-07-21 at 14.27.59.png]]
