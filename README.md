PUT https://petstore.swagger.io/v2/pet 

pm.test("Status code 200", function () {
    pm.expect(pm.response).to.have.status(200);
});

pm.test("Response time", function () {
    pm.expect(pm.response.responseTime).to.be.below(200); 
});

pm.test("Error if incorrect data types", function () {
    if (pm.response.code === 400) 
        const responseBody = pm.response.json();
        pm.expect(responseBody.message).to.include("Parameter value must be valid");
    }
});

pm.test("Error if invalid field values", function () {
    const invalidStatuses = ['unknown', 'invalidStatus'];
    if (pm.response.code === 400) 
        const responseBody = pm.response.json();
        pm.expect(responseBody.message).to.include("invalid value");
    }
});

const requiredFields = ["name", "status", "id"];
pm.test("Required fields are missing", function () {
    if (pm.response.code === 400) {
        const responseBody = pm.response.json();
        requiredFields.forEach(field => {
            pm.expect(responseBody.message).to.include(field);
        });
    }
});


pm.test("Minimum variable values", function () {
    pm.expect(pm.response).to.have.status(200);
    const responseBody = pm.response.json();
    pm.expect(responseBody.category.id).to.be.at.least(1); 
});

// The test should be written for each field with appropriate data type and field restriction

pm.test("Maximum variable values", function () {
    pm.expect(pm.response).to.have.status(200); 
    const responseBody = pm.response.json();
    pm.expect(responseBody.category.id).to.be.below(9223372036854775808); 
});

// The test should be written for each field with appropriate data type and field restriction

const validStatuses = ['available', 'pending', 'sold'];
pm.test("Status is valid", function () {
    const status = pm.environment.get("randomStatus");
    pm.expect(validStatuses).to.include(status);
});


const imageFiles = pm.environment.get("imageFiles")
imageFiles.forEach((file, index) => {
    pm.sendRequest({
        url: ${pm.environment.get("baseURL")}/pet/${petId}/uploadImage}
function (err, res) {
        pm.test(Status 200 for image upload ${index + 1}, function () {
        pm.expect(res).to.have.property("status", 200);
        });



pm.sendRequest({
    url: `${pm.environment.get("baseURL")}/pet/${petId}/uploadImage`
    }
}, function (err, res) {
    pm.test("Status 400 returned for invalid file type", function () {
        pm.expect(res).to.have.property("status", 400);
        const jsonData = res.json();
        pm.expect(jsonData.message).to.include("unsupported file type");
    });
});
