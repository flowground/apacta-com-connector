# ![LOGO](logo.png) Apacta **flow**ground Connector

## Description

A generated **flow**ground connector for the Apacta API (version 0.0.1).

Generated from: https://api.apis.guru/v2/specs/apacta.com/0.0.1/swagger.json<br/>
Generated at: 2019-05-07T17:36:35+03:00

## API Description

API for a tool to craftsmen used to register working hours, material usage and quality assurance.    
# Endpoint
The endpoint `https://app.apacta.com/api/v1` should be used to communicate with the API. API access is only allowed with SSL encrypted connection (https).
# Authentication
URL query authentication with an API key is used, so appending `?api_key={api_key}` to the URL where `{api_key}` is found within Apacta settings is used for authentication
# Pagination
If the endpoint returns a `pagination` object it means the endpoint supports pagination - currently it's only possible to change pages with `?page={page_number}` but implementing custom page sizes are on the road map.


# Search/filter
Is experimental but implemented in some cases - see the individual endpoints' docs for further explanation.
# Ordering
Is currently experimental, but on some endpoints it's implemented on URL querys so eg. to order Invoices by `invoice_number` appending `?sort=Invoices.invoice_number&direction=desc` would sort the list descending by the value of `invoice_number`.
# Associations
Is currently implemented on an experimental basis where you can append eg. `?include=Contacts,Projects`  to the `/api/v1/invoices/` endpoint to embed `Contact` and `Project` objects directly.
# Project Files
Currently project files can be retrieved from two endpoints. `/projects/{project_id}/files` handles files uploaded from wall posts or forms. `/projects/{project_id}/project_files` allows uploading and showing files, not belonging to specific form or wall post.
# Errors/Exceptions
## 422 (Validation)
Write something about how the `errors` object contains keys with the properties that failes validation like:
```
  {
      "success": false,
      "data": {
          "code": 422,
          "url": "/api/v1/contacts?api_key=5523be3b-30ef-425d-8203-04df7caaa93a",
          "message": "A validation error occurred",
          "errorCount": 1,
          "errors": {
              "contact_types": [ ## Property name that failed validation
                  "Contacts must have at least one contact type" ## Message with further explanation
              ]
          }
      }
  }
```
## Code examples
Running examples of how to retrieve the 5 most recent forms registered and embed the details of the User that made the form, and eventual products contained in the form
### Swift
```
  
```
### Java
#### OkHttp
```
  OkHttpClient client = new OkHttpClient();
  
  Request request = new Request.Builder()
    .url("https://app.apacta.com/api/v1/forms?extended=true&sort=Forms.created&direction=DESC&include=Products%2CCreatedBy&limit=5")
    .get()
    .addHeader("x-auth-token", "{INSERT_YOUR_TOKEN}")
    .addHeader("accept", "application/json")
    .build();
  
  Response response = client.newCall(request).execute();
```
#### Unirest
```
  HttpResponse<String> response = Unirest.get("https://app.apacta.com/api/v1/forms?extended=true&sort=Forms.created&direction=DESC&include=Products%2CCreatedBy&limit=5")
    .header("x-auth-token", "{INSERT_YOUR_TOKEN}")
    .header("accept", "application/json")
    .asString();
```
### Javascript
#### Native
```
  var data = null;
  
  var xhr = new XMLHttpRequest();
  xhr.withCredentials = true;
  
  xhr.addEventListener("readystatechange", function () {
    if (this.readyState === 4) {
      console.log(this.responseText);
    }
  });
  
  xhr.open("GET", "https://app.apacta.com/api/v1/forms?extended=true&sort=Forms.created&direction=DESC&include=Products%2CCreatedBy&limit=5");
  xhr.setRequestHeader("x-auth-token", "{INSERT_YOUR_TOKEN}");
  xhr.setRequestHeader("accept", "application/json");
  
  xhr.send(data);
```
#### jQuery
```
  var settings = {
    "async": true,
    "crossDomain": true,
    "url": "https://app.apacta.com/api/v1/forms?extended=true&sort=Forms.created&direction=DESC&include=Products%2CCreatedBy&limit=5",
    "method": "GET",
    "headers": {
      "x-auth-token": "{INSERT_YOUR_TOKEN}",
      "accept": "application/json",
    }
  }
  
  $.ajax(settings).done(function (response) {
    console.log(response);
  });
```
#### NodeJS (Request)
```
  var request = require("request");

  var options = { method: 'GET',
    url: 'https://app.apacta.com/api/v1/forms',
    qs: 
     { extended: 'true',
       sort: 'Forms.created',
       direction: 'DESC',
       include: 'Products,CreatedBy',
       limit: '5' },
    headers: 
     { accept: 'application/json',
       'x-auth-token': '{INSERT_YOUR_TOKEN}' } };
  
  request(options, function (error, response, body) {
    if (error) throw new Error(error);
  
    console.log(body);
  });

```
### Python 3
```
  import http.client
  
  conn = http.client.HTTPSConnection("app.apacta.com")
  
  payload = ""
  
  headers = {
      'x-auth-token': "{INSERT_YOUR_TOKEN}",
      'accept': "application/json",
      }
  
  conn.request("GET", "/api/v1/forms?extended=true&sort=Forms.created&direction=DESC&include=Products%2CCreatedBy&limit=5", payload, headers)
  
  res = conn.getresponse()
  data = res.read()
  
  print(data.decode("utf-8"))
```
### C#
#### RestSharp
```
  var client = new RestClient("https://app.apacta.com/api/v1/forms?extended=true&sort=Forms.created&direction=DESC&include=Products%2CCreatedBy&limit=5");
  var request = new RestRequest(Method.GET);
  request.AddHeader("accept", "application/json");
  request.AddHeader("x-auth-token", "{INSERT_YOUR_TOKEN}");
  IRestResponse response = client.Execute(request);    
```
### Ruby
```
  require 'uri'
  require 'net/http'
  
  url = URI("https://app.apacta.com/api/v1/forms?extended=true&sort=Forms.created&direction=DESC&include=Products%2CCreatedBy&limit=5")
  
  http = Net::HTTP.new(url.host, url.port)
  http.use_ssl = true
  http.verify_mode = OpenSSL::SSL::VERIFY_NONE
  
  request = Net::HTTP::Get.new(url)
  request["x-auth-token"] = '{INSERT_YOUR_TOKEN}'
  request["accept"] = 'application/json'
  
  response = http.request(request)
  puts response.read_body
```
### PHP (HttpRequest)
```
  <?php

  $request = new HttpRequest();
  $request->setUrl('https://app.apacta.com/api/v1/forms');
  $request->setMethod(HTTP_METH_GET);
  
  $request->setQueryData(array(
    'extended' => 'true',
    'sort' => 'Forms.created',
    'direction' => 'DESC',
    'include' => 'Products,CreatedBy',
    'limit' => '5'
  ));
  
  $request->setHeaders(array(
    'accept' => 'application/json',
    'x-auth-token' => '{INSERT_YOUR_TOKEN}'
  ));
  
  try {
    $response = $request->send();
  
    echo $response->getBody();
  } catch (HttpException $ex) {
    echo $ex;
  }
```
### Shell (cURL)
```

  $ curl --request GET --url 'https://app.apacta.com/api/v1/forms?extended=true&sort=Forms.created&direction=DESC&include=Products%2CCreatedBy&limit=5' --header 'accept: application/json' --header 'x-auth-token: {INSERT_YOUR_TOKEN}'
  
```

## Authorization

Supported authorization schemes:
- API Key- API Key
## Actions

### Get list of cities supported in Apacta

*Tags:* `Cities`

#### Input Parameters
* `zip_code` - _optional_ - Used to search for a city with specific zip code

### Get details about one city

*Tags:* `Cities`

#### Input Parameters
* `city_id` - _required_

### Get a list of clocking records

*Tags:* `ClockingRecords`

#### Input Parameters
* `active` - _optional_ - Used to search for active clocking records

### Create clocking record for authenticated user

*Tags:* `ClockingRecords`

### Checkout active clocking record for authenticated user

*Tags:* `ClockingRecords`

### Delete a clocking record

*Tags:* `ClockingRecords`

#### Input Parameters
* `clocking_record_id` - _required_

### Details of 1 clocking_record

*Tags:* `ClockingRecords`

#### Input Parameters
* `clocking_record_id` - _required_

### Edit a clocking record

*Tags:* `ClockingRecords`

#### Input Parameters
* `clocking_record_id` - _required_

### Get a list of companies

*Tags:* `Companies`

### Details of 1 company

*Tags:* `Companies`

#### Input Parameters
* `company_id` - _required_

### Get a list of integration feature settings

*Tags:* `Companies`

#### Input Parameters
* `company_id` - _required_

### Show details of 1 integration feature setting

*Tags:* `Companies`

#### Input Parameters
* `company_id` - _required_
* `integration_feature_setting_id` - _required_

### Get list of contact types supported in Apacta

*Tags:* `ContactTypes`

#### Input Parameters
* `identifier` - _optional_ - Search for specific identifier value

### Get details about one contact type

*Tags:* `ContactTypes`

#### Input Parameters
* `contact_type_id` - _required_

### Get a list of contacts

*Tags:* `Contacts`

#### Input Parameters
* `name` - _optional_ - Used to search for a contact with a specific name
* `cvr` - _optional_ - Search for values in CVR field
* `ean` - _optional_ - Search for values in EAN field
* `erp_id` - _optional_ - Search for values in ERP id field
* `contact_type` - _optional_ - Used to show only contacts with with one specific `ContactType`
* `city` - _optional_ - Used to show only contacts with with one specific `City`

### Add a new contact

*Tags:* `Contacts`

### Delete a contact

*Tags:* `Contacts`

#### Input Parameters
* `contact_id` - _required_

### Details of 1 contact

*Tags:* `Contacts`

#### Input Parameters
* `contact_id` - _required_

### Edit a contact

*Tags:* `Contacts`

#### Input Parameters
* `contact_id` - _required_

### Get list of currencies supported in Apacta

*Tags:* `Currencies`

### Get details about one currency

*Tags:* `Currencies`

#### Input Parameters
* `currency_id` - _required_

### Used to retrieve details about the logged in user's hours

*Tags:* `EmployeeHours`

#### Input Parameters
* `date_from` - _required_ - Date formatted as Y-m-d (2016-06-28)
* `date_to` - _required_ - Date formatted as Y-m-d (2016-06-28)

### Show list of expense files

*Tags:* `ExpenseFiles`

#### Input Parameters
* `created_by_id` - _optional_
* `expense_id` - _optional_

### Add file to expense

*Tags:* `ExpenseFiles`

### Delete file

*Tags:* `ExpenseFiles`

#### Input Parameters
* `expense_file_id` - _required_

### Show file

*Tags:* `ExpenseFiles`

#### Input Parameters
* `expense_file_id` - _required_

### Edit file

*Tags:* `ExpenseFiles`

#### Input Parameters
* `expense_file_id` - _required_

### Show list of expense lines

*Tags:* `ExpenseLines`

#### Input Parameters
* `created_by_id` - _optional_
* `currency_id` - _optional_
* `expense_id` - _optional_

### Add line to expense

*Tags:* `ExpenseLines`

### Delete expense line

*Tags:* `ExpenseLines`

#### Input Parameters
* `expense_line_id` - _required_

### Show expense line

*Tags:* `ExpenseLines`

#### Input Parameters
* `expense_line_id` - _required_

### Edit expense line

*Tags:* `ExpenseLines`

#### Input Parameters
* `expense_line_id` - _required_

### Show list of expenses

*Tags:* `Expenses`

#### Input Parameters
* `created_by_id` - _optional_
* `company_id` - _optional_
* `contact_id` - _optional_
* `project_id` - _optional_
* `gt_created` - _optional_ - Created after date
* `lt_created` - _optional_ - Created before date

### Add line to expense

*Tags:* `Expenses`

### Delete expense

*Tags:* `Expenses`

#### Input Parameters
* `expense_id` - _required_

### Show expense

*Tags:* `Expenses`

#### Input Parameters
* `expense_id` - _required_

### Edit expense

*Tags:* `Expenses`

#### Input Parameters
* `expense_id` - _required_

### Show list of all OIOUBL files for the expense

*Tags:* `Expense OIOUBL files`

#### Input Parameters
* `expense_id` - _required_

### Show OIOUBL file

*Tags:* `Expense OIOUBL files`

#### Input Parameters
* `expense_id` - _required_
* `file_id` - _required_

### Get list of form field types

*Tags:* `FormFieldTypes`

#### Input Parameters
* `name` - _optional_ - Used to filter on the `name` of the form_fields
* `identifier` - _optional_ - Used to filter on the `identifier` of the form_fields

### Get details about single `FormField`

*Tags:* `FormFieldTypes`

#### Input Parameters
* `form_field_type_id` - _required_

### Add a new field to a `Form`

*Tags:* `FormFields`

### Get details about single `FormField`

*Tags:* `FormFields`

#### Input Parameters
* `form_field_id` - _required_

### Get array of form_templates for your company

*Tags:* `FormTemplates`

#### Input Parameters
* `name` - _optional_ - Used to filter on the `name` of the form_templates
* `identifier` - _optional_ - Used to filter on the `identifier` of the form_templates
* `pdf_template_identifier` - _optional_ - Used to filter on the `pdf_template_identifier` of the form_templates
* `description` - _optional_ - Used to filter on the `description` of the form_templates

### View one form template

*Tags:* `FormTemplates`

#### Input Parameters
* `form_template_id` - _required_

### Retrieve array of forms

*Tags:* `Forms`

#### Input Parameters
* `extended` - _optional_ - Used to have extended details from the forms from the `Form`'s `FormFields`
    Possible values: true, false.
* `date_from` - _optional_ - Used in conjunction with `date_to` to only show forms within these dates - format like `2016-28-05`
* `date_to` - _optional_ - Used in conjunction with `date_from` to only show forms within these dates - format like `2016-28-30`
* `project_id` - _optional_ - Used to filter on the `project_id` of the forms
* `created_by_id` - _optional_ - Used to filter on the `created_by_id` of the forms
* `form_template_id` - _optional_ - Used to filter on the `form_template_id` of the forms

### Add new form

> Used to add a form into the system

*Tags:* `Forms`

### Delete a form

> You can only delete the forms that you've submitted yourself

*Tags:* `Forms`

#### Input Parameters
* `form_id` - _required_

### View form

*Tags:* `Forms`

#### Input Parameters
* `form_id` - _required_

### Edit a form

*Tags:* `Forms`

#### Input Parameters
* `form_id` - _required_

### View list of invoice lines

*Tags:* `InvoiceLines`

#### Input Parameters
* `invoice_id` - _optional_
* `product_id` - _optional_
* `user_id` - _optional_
* `name` - _optional_
* `discount_text` - _optional_

### Add invoice

*Tags:* `InvoiceLines`

### Delete invoice line

*Tags:* `InvoiceLines`

#### Input Parameters
* `invoice_line_id` - _required_

### View invoice line

*Tags:* `InvoiceLines`

#### Input Parameters
* `invoice_line_id` - _required_

### Edit invoice line

*Tags:* `InvoiceLines`

#### Input Parameters
* `invoice_line_id` - _required_

### View list of invoices

*Tags:* `Invoices`

#### Input Parameters
* `contact_id` - _optional_ - Used to filter on the `contact_id` of the invoices
* `project_id` - _optional_ - Used to filter on the `project_id` of the invoices
* `invoice_number` - _optional_ - Used to filter on the `invoice_number` of the invoices
* `offer_number` - _optional_
* `is_draft` - _optional_
    Possible values: 0, 1.
* `is_offer` - _optional_
    Possible values: 0, 1.
* `is_locked` - _optional_
    Possible values: 0, 1.
* `date_from` - _optional_
* `date_to` - _optional_
* `issued_date` - _optional_

### Add invoice

*Tags:* `Invoices`

### Delete invoice

*Tags:* `Invoices`

#### Input Parameters
* `invoice_id` - _required_

### View invoice

*Tags:* `Invoices`

#### Input Parameters
* `invoice_id` - _required_

### Edit invoice

*Tags:* `Invoices`

#### Input Parameters
* `invoice_id` - _required_

### View list of mass messages for specific user

*Tags:* `MassMessagesUsers`

#### Input Parameters
* `is_read` - _optional_ - Used to filter on the `is_read` of the mass messages

### View mass message

*Tags:* `MassMessagesUsers`

#### Input Parameters
* `mass_messages_user_id` - _required_

### Edit mass message

*Tags:* `MassMessagesUsers`

#### Input Parameters
* `mass_messages_user_id` - _required_

### View list of all materials

*Tags:* `Materials`

#### Input Parameters
* `barcode` - _optional_ - Used to filter on the `barcode` of the materials
* `name` - _optional_ - Used to filter on the `name` of the materials
* `project_id` - _optional_ - Used to find materials used in specific project by `project_id`
* `currently_rented` - _optional_ - Used to find currently rented materials

### Delete material

*Tags:* `Materials`

#### Input Parameters
* `material_id` - _required_

### View material

*Tags:* `Materials`

#### Input Parameters
* `material_id` - _required_

### Edit material

*Tags:* `Materials`

#### Input Parameters
* `material_id` - _required_

### Show list of rentals for specific material

*Tags:* `MaterialRentals`

#### Input Parameters
* `material_id` - _required_

### Add material rental

*Tags:* `MaterialRentals`

#### Input Parameters
* `material_id` - _required_

### Checkout material rental

*Tags:* `MaterialRentals`

#### Input Parameters
* `material_id` - _required_

### Delete material rental

> Delete rental for material

*Tags:* `MaterialRentals`

#### Input Parameters
* `material_id` - _required_
* `material_rental_id` - _required_

### Show rental foor materi

*Tags:* `MaterialRentals`

#### Input Parameters
* `material_id` - _required_
* `material_rental_id` - _required_

### Add material

*Tags:* `Materials`

#### Input Parameters
* `material_id` - _required_
* `material_rental_id` - _required_

### Edit material rental

*Tags:* `MaterialRentals`

#### Input Parameters
* `material_id` - _required_
* `material_rental_id` - _required_

### Get a list of payment term types

*Tags:* `PaymentTermTypes`

### Details of 1 payment term type

*Tags:* `PaymentTermTypes`

#### Input Parameters
* `payment_term_type_id` - _required_

### Get a list of payment terms

*Tags:* `PaymentTerms`

### Details of 1 payment term

*Tags:* `PaymentTerms`

#### Input Parameters
* `payment_term_id` - _required_

### Check if API is up and API key works

*Tags:* `Ping`

### List products

*Tags:* `Products`

#### Input Parameters
* `name` - _optional_ - Used to filter on the `name` of the products
* `product_number` - _optional_ - Used to filter on the `product_number` of the products
* `barcode` - _optional_ - Used to filter on the `barcode` of the products

### Add new product

*Tags:* `Products`

### Delete a product

*Tags:* `Products`

#### Input Parameters
* `product_id` - _required_

### View single product

*Tags:* `Products`

#### Input Parameters
* `product_id` - _required_

### Edit a product

*Tags:* `Products`

#### Input Parameters
* `product_id` - _required_

### Get list of project statuses

*Tags:* `ProjectStatuses`

### Get details about one contact type

*Tags:* `ProjectStatuses`

#### Input Parameters
* `project_status_id` - _required_

### View list of projects

*Tags:* `Projects`

#### Input Parameters
* `show_all` - _optional_ - Unless this is set to `true` only open projects will be shown
* `contact_id` - _optional_ - Used to filter on the `contact_id` of the projects
* `project_status_id` - _optional_ - Used to filter on the `project_status_id` of the projects
* `project_status_ids` - _optional_ - Used to filter on the `project_status_id` of the projects (match any of the provided values)
* `name` - _optional_ - Used to search on the `name` of the projects
* `erp_project_id` - _optional_ - Used to search on the `erp_project_id` of the projects
* `erp_task_id` - _optional_ - Used to search on the `erp_task_id` of the projects
* `start_time_gte` - _optional_ - Show projects with start time after than this value
* `start_time_lte` - _optional_ - Show projects with start time before this value
* `start_time_eq` - _optional_ - Show only projects with start time on specific date

### Add a project

*Tags:* `Projects`

### Delete a project

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_

### View specific project

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_

### Edit a project

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_

### Show list of files uploaded to project

> Used to show files uploaded to a project from wall post or form

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_

### Delete file

> Delete file uploaded to a project from wall post or form

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_
* `file_id` - _required_

### Show file

> Show file uploaded to a project from wall post or form

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_
* `file_id` - _required_

### Edit file

> Edit file uploaded to a project from wall post or form

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_
* `file_id` - _required_

### Show list of project files uploaded to project

> Returns files belonging to the project, not uploaded from wall post or form

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_

### Add project file to projects

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_

### Delete project file

*Tags:* `Projects`

#### Input Parameters
* `project_file_id` - _required_
* `project_id` - _required_

### Show project file

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_
* `project_file_id` - _required_

### Edit project file

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_
* `project_file_id` - _required_

### Show list of users added to project

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_

### Add user to project

*Tags:* `Projects`

#### Input Parameters
* `project_id` - _required_

### Delete user from project

*Tags:* `Projects`

#### Input Parameters
* `user_id` - _required_
* `project_id` - _required_

### View specific user assigned to project

*Tags:* `Projects`

#### Input Parameters
* `user_id` - _required_
* `project_id` - _required_

### List stock_locations

*Tags:* `StockLocations`

#### Input Parameters
* `name` - _optional_ - Used to filter on the `name` of the stock_locations

### Add new stock_locations

*Tags:* `StockLocations`

### Delete location

*Tags:* `StockLocations`

#### Input Parameters
* `location_id` - _required_

### View single location

*Tags:* `StockLocations`

#### Input Parameters
* `location_id` - _required_

### Edit location

*Tags:* `StockLocations`

#### Input Parameters
* `location_id` - _required_

### List time entries

*Tags:* `TimeEntries`

#### Input Parameters
* `user_id` - _optional_
* `form_id` - _optional_
* `project_id` - _optional_
* `gt_from_time` - _optional_
* `lt_from_time` - _optional_
* `gt_to_time` - _optional_
* `lt_to_time` - _optional_
* `lt_sum` - _optional_
* `gt_sum` - _optional_

### Add new time entry

*Tags:* `TimeEntries`

### Delete time entry

*Tags:* `TimeEntries`

#### Input Parameters
* `time_entry_id` - _required_

### View time entry

*Tags:* `TimeEntries`

#### Input Parameters
* `time_entry_id` - _required_

### Edit time entry

*Tags:* `TimeEntries`

#### Input Parameters
* `time_entry_id` - _required_

### List possible time entry intervals

*Tags:* `TimeEntryIntervals`

### View time entry interval

*Tags:* `TimeEntryIntervals`

#### Input Parameters
* `time_entry_interval_id` - _required_

### List time entries types

*Tags:* `TimeEntryTypes`

### Add new time entry type

*Tags:* `TimeEntryTypes`

### Delete time entry type

*Tags:* `TimeEntryTypes`

#### Input Parameters
* `time_entry_type_id` - _required_

### View time entry type

*Tags:* `TimeEntryTypes`

#### Input Parameters
* `time_entry_type_id` - _required_

### Edit time entry type

*Tags:* `TimeEntryTypes`

#### Input Parameters
* `time_entry_type_id` - _required_

### List possible time entry unit types

*Tags:* `TimeEntryUnitTypes`

### View time entry unit type

*Tags:* `TimeEntryUnitTypes`

#### Input Parameters
* `time_entry_unit_type_id` - _required_

### List possible time entry value types

*Tags:* `TimeEntryValueTypes`

### View time entry value type

*Tags:* `TimeEntryValueTypes`

#### Input Parameters
* `time_entry_value_type_id` - _required_

### Get list of users in company

*Tags:* `Users`

#### Input Parameters
* `first_name` - _optional_ - Used to filter on the `first_name` of the users
* `last_name` - _optional_ - Used to filter on the `last_name` of the users
* `email` - _optional_ - Used to filter on the `email` of the users
* `stock_location_id` - _optional_ - Used to filter on the `stock_location_id` of the users

### Add user to company

*Tags:* `Users`

### Delete user

*Tags:* `Users`

#### Input Parameters
* `user_id` - _required_

### View user

*Tags:* `Users`

#### Input Parameters
* `user_id` - _required_

### Edit user

*Tags:* `Users`

#### Input Parameters
* `user_id` - _required_

### List vendor products

*Tags:* `VendorProducts`

#### Input Parameters
* `name` - _optional_ - Used to filter on the `name` of the vendor products
* `product_number` - _optional_ - Used to filter on the `product_number` of the vendor products
* `barcode` - _optional_ - Used to filter on the `barcode` of the vendor products
* `vendor_id` - _optional_ - Used to filter on the `vendor_id` of the vendor products

### View single vendor product

*Tags:* `VendorProducts`

#### Input Parameters
* `vendor_product_id` - _required_

### Add wall comment

*Tags:* `WallComments`

### View wall comment

*Tags:* `WallComments`

#### Input Parameters
* `wall_comment_id` - _required_

### View list of wall posts

*Tags:* `WallPosts`

#### Input Parameters
* `project_id` - _required_
* `user_id` - _optional_

### Add a wall post

*Tags:* `WallPosts`

### View wall post

*Tags:* `WallPosts`

#### Input Parameters
* `wall_post_id` - _required_

### See wall comments to a wall post

*Tags:* `WallPosts`

#### Input Parameters
* `wall_post_id` - _required_

## License

**flow**ground :- Telekom iPaaS / apacta-com-connector<br/>
Copyright © 2019, [Deutsche Telekom AG](https://www.telekom.de)<br/>
contact: flowground@telekom.de

All files of this connector are licensed under the Apache 2.0 License. For details
see the file LICENSE on the toplevel directory.
