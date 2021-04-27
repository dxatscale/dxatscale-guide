# Utilizing Callable Interface

## Overview

There's a need to occasionally communicate to non dependent packages without directly depending on it. One such method is to utilize callable interface, a native Salesforce apex mechanism which can be used to invert dependencies between packages.

> It  enables developers to use a common interface to build loosely coupled integrations between Apex classes or triggers, even for code in separate packages. Agreeing upon a common interface enables developers from different companies or different departments to build upon one another’s solutions. Implement this interface to enable the broader community, which might have different solutions than the ones you had in mind, to extend your code’s functionality



### Scenario:

Access Product Role object which is hosted in an upstream  package in the products domain which is not accessible by downstream packages in customer domain.  A Product Role interface needs to be built within upstream product packages to return the IDs of product holding information based on customer ID and product role, which need to be consumed by the packages in customer domain

### Code example:

To solve the above scneario, the following implementation needs to be added to the package in the product domain. 

```text
public class ProductRoleCallable implements Callable {

// Actual method to return a map <customerID, map <product role as string, ali as object>>

 Map<ID, Map< String, assetlineitem obj> getProductHoldingbyRole(List<AccountID> lstAcc){

 xxxxxxx
 return Map<ID, Map< String (role value), assetlineitem obj>;
 }

// Actual method to return xxx for something else needed from product package
 List<Agreement> getAgreements(List <AccountID> lstAcc){

  xxxxxxx
  return List<Agreement>;

 }


// To call specific methods dynamically
 public Object call(String action, Map<String, Object> args) {
     Switch on action {
    when 'productroleALI' {
     return this.getProductHoldingbyRole((List)args.get('lstAcc'));
    }

    when 'agreement' {
     return this.getAgreements((List)args.get('lstAcc'));
    }

    when else {
      throw new ExtensionMalformedCallException('Method not  implemented');
      }

     }
    }
// To throw exceptions
 public class ExtensionMalformedCallException extends Exception {}
 }
```

By utilizing the callable mechanism in package in the customer domain, once could directly access the functionality provided by a non-dependent package

```text
Map<ID, Map< role, assetlineitem obj> result = new Map<ID, Map< role, assetlineitem obj>();
list<ID> lstAcc = new List<ID>();
// Instantiate ProductRoleCallable class
Callable c=(Callable)Type.forName('ProductRoleCallable').newInstance();
result= c.call('productroleALI', new Map < String, Object > {'lstAcc' => lstAcc}));
```

Reference: Salesforce Documentation: [https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex\_interface\_System\_Callable.htm](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_interface_System_Callable.htm)

