# Postman-Testovoe-
### Writing tests.
 *Tests in Postman make sure the API works as expected. The folowing Snippets was used in my homeworks*:

:small_orange_diamond: Testing status codes.

    If the response code is 200, the test will pass, otherwise it will fail.
```js
    pm.test("Status code is 200",           function () {
        pm.response.to.have.status(200);
    });
    pm.test("Status code name has OK",  function () {
     pm.response.to.have.status("OK");
});
```
:small_orange_diamond: Test if the response body contains a string:
```pm.test("Body matches string", function () {
    pm.expect(pm.response.text()).to.include("string_you_want_to_search");
});
```
:small_orange_diamond:  Parsing response body data.
```js 
responseJson = pm.response.json();
```
:small_orange_diamond: Parsing request form data 
```js
var req = request.data
```
:small_orange_diamond: Parsing request from method Get
```js
var req = pm.request. url.query.toObject();
```
:small_orange_diamond: Testing response body eql req
```js
pm.test("Your test name", function () {
    pm.expect(jsonData.value).to.eql(reqData.value);
});
```
:small_orange_diamond: Set the an environment variable
```js
pm.environment.set("variable_key", "variable_value");
```
:small_orange_diamond: headers
```js
pm.test("Content-Type header is present", () => {
  pm.response.to.have.header("Content-Type");
});

pm.test("Content-Type header is application/json", () => {
  pm.expect(pm.response.headers.get('Content-Type')).to.eql('application/json');
});

pm.test("Check Cookie is not present", () => {
  pm.expect(pm.cookies.has('JSESSIONID')).to.be.false;
});

pm.test("Check Cookie is presen", () => {
   pm.expect(pm.cookies.has('JSESSIONID')).to.be.true;
});
```

:small_orange_diamond: array
```js
pm.test("response have array", () => {
  pm.expect(jsonData).to.be.an("array");
});

// jsonData.not.null
pm.test("jsonData.not.null", () => {
    pm.expect(jsonData).to.be.not.null;
});
```
:small_orange_diamond: check value jsonData
```js
const keyisInJson = ['content','id','publication_datetime','title','author']

jsonData.forEach(elemnt =>
keyisInJson.forEach(key => {
    pm.test(`Response has ${key}`, () => {
        pm.expect(elemnt).to.have.property(key)
    })
}));

jsonData.forEach(elemnt => {
    pm.test(`elemnt.content is string`, () => {
        pm.expect(elemnt.content).to.be.a('string');
    })
});

jsonData.forEach(elemnt => {
    pm.test(`elemnt.id is number`, () => {
        pm.expect(elemnt.id).to.be.a('number');
    })
});

jsonData.forEach(elemnt => {
    pm.test(`elemnt.publication_datetime is string`, () => {
        pm.expect(elemnt.publication_datetime).to.be.a('string');
    })
});
```

:small_orange_diamond: check value jsonData
```js
const content = pm.iterationData.get('content');
const title = pm.iterationData.get('title'); // old
const name = pm.iterationData.get('name'); // new

function contentValidation(value) {
    return value && value.lenght > 3 && value.lenght <= 180 && value.trim() == value
}

function titleValidation(value) {
    return value && value.lenght > 3 && value.lenght <= 80 && value.trim() == value
}

function  validate(content,title) {
    return contentValidation(content) && nameValidation(title)
}
if (validate(content,title)) {

    pm.test(`ne 201 code with content == ${content} and title == ${title} `, () => {
        pm.response.to.not.have.status(201);
    })
} else {
    pm.test(`201 code with content == ${content} and title == ${title} `, () => {
        pm.response.to.have.status(201);
    })
}
```
### We continue to write tests in Postman. Learning Json Schema.
*JSON Schema is a vocabulary that allows you to annotate and validate JSON documents*.
*I used the following tool to convert Json to Json Schema*:

:link: https://www.convertsimple.com/convert-json-to-json-schema/
