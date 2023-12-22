# woku API Documentation | Endpoint to Create a woku (Version v0.0)

This service is part of woku SpA: woku is a tool for capturing 1 to 5 star ratings and customer opinions in text or audio format on products or services of a company.

### Important Considerations

This documentation is a practical example for RE/MAX of what the woku client API would be like, since the domain api-client.woku.app is not active, as the project is under development.

## Introduction

### General Description
This is a REST API service that enables company owners within the woku service to create wokus and other functions. For this purpose, only the endpoint for creating a woku is described.

#### Base URL
`https://api-client.woku.app`

## Authentication

### Type of Authentication
Company application key.

### Obtaining and Using Keys
A company application key is provided to the company owner in woku. This key must be included in the headers of API requests.
The secondaryKey is created and obtained in the folders of a company in woku through the woku client interface.
The woku client interface can be accessed at `https://fresh.woku.app`

## Endpoint to Create wokus

### URL
`/create-woku`

### Method
POST

### Headers
- `Content-Type: application/json`
- `Authorization: Bearer <company_application_key>`

### Body Request
```json
{
  "description": "Wall painting service",
  "file": "https://wokudevfiles.blob.core.windows.net/wokus/cd7f9cf3-c2e4-4ff0-8a96-19ff813f569e1699220394936-image.webp",
  "secondaryKey": "6580244e98ebf3609b1b2c2f",
  "clientEmail": "diego@woku.app",
  "clientPhone": 56912341234
}
```

### Expected Responses
- `200 OK: Woku created successfully.`
- `401 Unauthorized: Invalid or missing application key.`
- `400 Bad Request: Invalid message body data.`

### DTO of the Body

#### CreateWokuDTO
- **description*** (string)
  - Example: Description of the woku
  - The description cannot have fewer than 3 characters and cannot exceed a maximum of 140 characters.
- **file*** (string)
  - This field must be a publicly accessible URL to an image or video file.
- **secondaryKey** (string)
  - This is an optional field. This key must be provided by the company owner to a company folder manually in the woku client interface.
- **clientEmail*** (string)
  - This field must contain a valid email.
- **clientPhone** (number)
  - This is an optional field. This field should only have consecutive numbers.
 
## Usage Examples

### JavaScript (using Fetch API)
```javascript
fetch('https://api-client.woku.app/create-woku', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': 'Bearer <your_application_key>'
    },
    body: JSON.stringify({
      description: "Description of the woku",
      file: "File URL",
      secondaryKey: "Secondary key",
      clientEmail: "Email",
      clientPhone: 123456789
    })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

### Python (using requests)
```python
import requests

url = 'https://api-client.woku.app/create-woku'
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'Bearer <your_application_key>'
}
data = {
  'description': 'Description of the woku',
  'file': 'File URL',
  'secondaryKey': 'Secondary key',
  'clientEmail': 'Email',
  'clientPhone': 123456789
}

response = requests.post(url, json=data, headers=headers)
print(response.json())
```

### PHP (using cURL)
```php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://api-client.woku.app/create-woku');
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
  'Content-Type: application/json',
  'Authorization: Bearer <your_application_key>'
));
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode(array(
  'description' => 'Description of the woku',
  'file' => 'File URL',
  'secondaryKey' => 'Secondary key',
  'clientEmail' => 'Email',
  'clientPhone' => 123456789
)));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($ch);
curl_close($ch);
echo $response;
```

## Contact and Support

### Contact
Diego Orrego Brito, CTO of woku
Email: diego@woku.app (Please include the company name in the subject and mention the API).

## Common Errors and Solutions
### Inaccessible File URL
Ensure that the URL of the provided file is publicly accessible. Our service needs to be able to access the file to create the woku.

### Secondary Key
The secondary key can only be used if the company owner previously created it in a company folder through the woku client interface.










