POST https://petstore.swagger.io/v2/pet 


### 1. **Verify API stability under high load**

- **Pre-conditions:** Postman Collection Runner is set up to simulate multiple requests (e.g., 1000 requests per second) for API endpoint.
- **Test Steps:**
1. Send a request with and dynamically change valid data including required fields.
2. Start the test and monitor the API’s response for:

**-Response Time:** Each request should return within a specified response time (200ms).
-**Status Codes:** return a status code of 200.

**Expected result:** The API responds within acceptable performance limits without significant degradation or errors.

---

### 2. Verify endpoint validates input data types.

- **Pre-conditions:** Pre-field required fields: id, name, status.
- **Post-conditions:** The response includes an error message for invalid types.
- **Test Steps:**
    1. Send a request with invalid data types for one or more fields:
    - Id: Set as a string instead of number.
    - Category id: Set as a string instead of number.
    - Tags id: Set as a string instead of number.
    - Name: Set a number or object instead of a string (e.g.123).
    - Category name: Set a number or boolean instead of a string (e.g. true/false).
    - Tags name: Set a number or object instead of a string.

**Expected result:** Verify the response status is 400, with error message “Parameter value must be valid.”

---

### 3. Verify error for status invalid field values.

- **Pre-conditions:** Pre-field required fields: id, name, status.
- **Test Steps:**
    1. Send a request with an invalid value for status (e.g. unknown).

**Expected result:** Verify the response status is 400, with error message “invalid value.”

---

### 4. **Check Required Fields**

- **Test Steps:**
    1. Send requests with one or more required fields missing (name, status, id).

**Expected result:** Verify that the response is a 400 status with error message “missing field(s)”.

---

**5.** **Verify Unique ID Constraint**

**Pre-conditions:** The first entry with “xyz” id is successfully created. 
                              Pre-field required fields: name, status.

**Test Steps:**

1. Send a request to create a second entry with a specific “xyz” id.

**Expected Result:** The response returns 400 status code, with an error message  “id must be unique.”

---

### 6. **Check the Minimum value for field and average value**

- **Pre-conditions:** Pre-field required fields: id, name, status.
- **Test Steps:**
    1. Send a request with fields with the minimum acceptable value.
    2. Send a request with fields with the any average acceptable value:
    - Id: (1-9,223,372,036,854,775,807).
    - Category id: (1-9,223,372,036,854,775,807).
    - Tags id: (1-9,223,372,036,854,775,807).
    - Name: (1-255).
    - Category name: (1-255).
    - Tags name: (1-255).
    - PhotoUrls: (12-2000).

**Expected Result:** Successful entry creation for both, 200 status code.

---

### 7.  **Check the Maximum value for field and over value**

- **Pre-conditions:** Pre-field required fields: id, name, status.
- **Test Steps:**
    1. Send a request with fields with the maximum acceptable value:
    2. Send a request with fields with the over acceptable value:
    - Id: (1-9,223,372,036,854,775,807).
    - Category id: (1-9,223,372,036,854,775,807).
    - Tags id: (1-9,223,372,036,854,775,807).
    - Name: (1-255).
    - Category name: (1-255).
    - Tags name: (1-255).
    - PhotoUrls: (12-2000).

**Expected Result:** 

-Successful entry creation, 200 status code for maximum acceptable value.

-400 status code, with an error message  "Value exceeds acceptable limit” for over acceptable value.

---

### 8 Ensure the status field  accepts only specific values.

- **Pre-conditions:** Pre-field required fields: id, name.
- **Test Steps:**
    1. Send a request with status set to an allowed value (available, pending, sold.).
    2. Send a request with status set to an invalid value (e.g. completed).

**Expected Result:** Verify that the response status is 400 with an error message "Incorrect status value”.

---

### 9.Check if few image at time upload is successful.

- **Pre-conditions:** Pre-field required fields: id, name, status.
- **Test Steps:**
    1. Send an image upload request with a few valid file type.
- **Expected Result:** Successful entry creation, 200 status code.

---

### **10.Invalid File Type error handling**

- **Pre-conditions:** Pre-field required fields: id, name, status.

**Test Case Steps:**

1. Send an image upload request with an unsupported file type.
- **Expected Result:** 400 status is returned with an error message for invalid file types.
